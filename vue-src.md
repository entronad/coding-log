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

