# ref

http://zhouweicsu.github.io/blog/2017/03/07/vue-2-0-reactivity/

https://github.com/zoro-web/blog/issues/2

https://github.com/aooy/blog/issues/2

# note

JavaScript对象可以分为两类：数据属性、访问器属性

数据属性具有[[Value]]这一特性，可直接定义

访问器属性没有[[Value]]这一特性，可有[[Get]]/[[Set]]特性，不可直接定义，必须用Object.defineProperty定义，访问器属性会覆盖同名数据属性

---

Node类型值-name：

1---Node.ELEMENT_NODE---标签名

2---Node.ATTRIBUTE_NODE

3---Node.TEXT_NODE

9---Node.DOCUMENT_NODE---'#document'

11---Node.DOCUMENT_FRAGMENT_NODE---'#document-fragment'

DocumentFragment的特点

- 轻量级的Document，可包含和控制节点，但不占用额外资源
- 通过document.createDocumentFragment()创建
- DocumentFragment本体及其中的节点不会出现在文档树中，不会在视图渲染，当把DocumentFragment节点插入文档树中其实是插入他的所有子节点，利用这一特性可将其作为仓库暂存大量要插入的元素，避免反复渲染


---

Vue示例的构造函数入口

src/core/instance/index.js

```
function Vue (options) {
  this._init(options)
}

initMixin(Vue)  // 混合进_init方法
stateMixin(Vue) // 定义实例的$data $props $set $delete $watch
eventsMixin(Vue)
lifecycleMixin(Vue)
renderMixin(Vue)
```

---

src\core\instance\init.js

```
export function initMixin (Vue: Class<Component>) {
  Vue.prototype._init = function (options?: Object) {
    const vm: Component = this
    
    initLifecycle(vm)
    initEvents(vm)
    initRender(vm)
    callHook(vm, 'beforeCreate')
    initInjections(vm) // resolve injections before data/props
    initState(vm)
    initProvide(vm) // resolve provide after data/props
    callHook(vm, 'created')

    if (vm.$options.el) {
      vm.$mount(vm.$options.el)
    }
  }
}
```

src\core\instance\lifecycle.js

```
export function callHook (vm: Component, hook: string) {
  const handlers = vm.$options[hook]
  if (handlers) {
    for (let i = 0, j = handlers.length; i < j; i++) {
      try {
        handlers[i].call(vm)
      } catch (e) {
        handleError(e, vm, `${hook} hook`)
      }
    }
  }
  if (vm._hasHookEvent) {
    vm.$emit('hook:' + hook)
  }
}
```

src\core\observer\index.js

---

src\core\instance\state.js

```
export function stateMixin (Vue: Class<Component>) {
  // flow somehow has problems with directly declared definition object
  // when using Object.defineProperty, so we have to procedurally build up
  // the object here.
  const dataDef = {}
  dataDef.get = function () { return this._data }
  const propsDef = {}
  propsDef.get = function () { return this._props }
  if (process.env.NODE_ENV !== 'production') {
    dataDef.set = function (newData: Object) {
      warn(
        'Avoid replacing instance root $data. ' +
        'Use nested data properties instead.',
        this
      )
    }
    propsDef.set = function () {
      warn(`$props is readonly.`, this)
    }
  }
  Object.defineProperty(Vue.prototype, '$data', dataDef)
  Object.defineProperty(Vue.prototype, '$props', propsDef)

  Vue.prototype.$set = set
  Vue.prototype.$delete = del

  Vue.prototype.$watch = function (
    expOrFn: string | Function,
    cb: any,
    options?: Object
  ): Function {
    const vm: Component = this
    if (isPlainObject(cb)) {
      return createWatcher(vm, expOrFn, cb, options)
    }
    options = options || {}
    options.user = true
    const watcher = new Watcher(vm, expOrFn, cb, options)
    if (options.immediate) {
      cb.call(vm, watcher.value)
    }
    return function unwatchFn () {
      watcher.teardown()
    }
  }
}
```

F:\Github\vue\src\core\observer\index.js

```
export function set (target: Array<any> | Object, key: any, val: any): any {
  if (Array.isArray(target) && typeof key === 'number') {
    target.length = Math.max(target.length, key)
    target.splice(key, 1, val)
    return val
  }
  if (hasOwn(target, key)) {
    target[key] = val
    return val
  }
  const ob = (target: any).__ob__
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== 'production' && warn(
      'Avoid adding reactive properties to a Vue instance or its root $data ' +
      'at runtime - declare it upfront in the data option.'
    )
    return val
  }
  if (!ob) {
    target[key] = val
    return val
  }
  defineReactive(ob.value, key, val)
  ob.dep.notify()
  return val
}

/**
 * Delete a property and trigger change if necessary.
 */
export function del (target: Array<any> | Object, key: any) {
  if (Array.isArray(target) && typeof key === 'number') {
    target.splice(key, 1)
    return
  }
  const ob = (target: any).__ob__
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== 'production' && warn(
      'Avoid deleting properties on a Vue instance or its root $data ' +
      '- just set it to null.'
    )
    return
  }
  if (!hasOwn(target, key)) {
    return
  }
  delete target[key]
  if (!ob) {
    return
  }
  ob.dep.notify()
}

export function defineReactive (
  obj: Object,
  key: string,
  val: any,
  customSetter?: Function
) {
  const dep = new Dep()

  const property = Object.getOwnPropertyDescriptor(obj, key)
  if (property && property.configurable === false) {
    return
  }

  // cater for pre-defined getter/setters
  const getter = property && property.get
  const setter = property && property.set

  let childOb = observe(val)
  Object.defineProperty(obj, key, {
    enumerable: true,
    configurable: true,
    get: function reactiveGetter () {
      const value = getter ? getter.call(obj) : val
      if (Dep.target) {
        dep.depend()
        if (childOb) {
          childOb.dep.depend()
        }
        if (Array.isArray(value)) {
          dependArray(value)
        }
      }
      return value
    },
    set: function reactiveSetter (newVal) {
      const value = getter ? getter.call(obj) : val
      /* eslint-disable no-self-compare */
      if (newVal === value || (newVal !== newVal && value !== value)) {
        return
      }
      /* eslint-enable no-self-compare */
      if (process.env.NODE_ENV !== 'production' && customSetter) {
        customSetter()
      }
      if (setter) {
        setter.call(obj, newVal)
      } else {
        val = newVal
      }
      childOb = observe(newVal)
      dep.notify()
    }
  })
}
```



响应式的实现

initData调用observe()方法返回ob = new Observer(value)：

observer对象

- 首先创建了一个 Dep 对象实例；
- 然后把自身 this 添加到 value 的 __ob__ 属性上；
- 最后对 value 的类型进行判断，如果是数组则观察数组，否则观察单个元素（要理解这一步是个递归过程，即 value 的元素如果符合条件也需要转化为 Observer 对象）。

用walk方法遍历boserve对象，调用defineReactive，其中定义了dep.depend()

Dep 则是 Observer 和 Watcher 之间的纽带。依赖收集完成后，当属性变化会执行主题对象（Observer）的`dep.notify` 方法，这个方法会遍历订阅者（Watcher）列表向其发送消息，Watcher 会执行 `run` 方法去更新视图

模板渲染的实现：

- compile 函数主要是将 template 转换为 AST，优化 AST，再将 AST 转换为 render函数；
- render函数 与数据通过 Watcher 产生关联；
- 在数据发生变化时调用 patch 函数，执行此 render 函数，生成新 VNode，与旧 VNode 进行 diff，最终更新 DOM 树。



