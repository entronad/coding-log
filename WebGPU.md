WebGPU的坐标系称为标准设备坐标系（NDC）是现代图形接口都采用的坐标空间；vertex shader output 的输出空间会被gpu裁剪到屏幕范围内，所以也被称为 clip space，坐标后面再添个1称为齐次坐标，vertex shader output也被称为齐次空间

贴图分三种：图像贴图，canvas贴图，video贴图，注意video贴图各方面都很不一样

多物体资源绑定有四种方法：buffers, buffer with offsets, dynamic offsets, instance

贴图可以使用一些更高效的新格式：webp, webp2, jpeg xl, avif

视频贴图可使用更高效的贴图：vp8/9, av1

可以用顶点索引定制三角，类似triangle-strip的压缩数据，但还是triangle-list模式

为了灵活，一般modelView矩阵和project矩阵是分别传入shader中在里面再组成mvp矩阵，以便与Camara矩阵分别处理

注意shader虽然是GPU计算，但它会被执行多次，所以不能指望太多东西在shader中计算，尽量在外面算好

由于mapAsnc的效率很低，所以要尽量减少GPU和CPU同步缓冲区的次数，可通过bindGroup在不同的管线中直接共享

多个管线串联中间只要end，最后encoder只submit一次

几乎每个对象都可以设置label，最好设置label，它在打印调试时很有用

如果module中@vertex和@fragment只有一个，pipeline定义中可以不写entryPoint

WebGPU绘制到textures上，canvas能够提供texture

location是指的参数位移，position是指的图上坐标

canvas缩放的时候不会改变分辨率，图形会有锯齿，因此当它缩放时，要重新设置 canvas.width height, 调用 context.getCurrentTexture()。这一过程一般通过ResizeObserver监视实现

adapter.requestDevice()总能获取到一个device，但能不能用通过 device.lost 触发，它是一个promise当丢失时resolve

注意vertex shader输出和fragment shader输入的@builtin(position)是完全不同的，fragment shader中是针对每一个像素点的像素坐标系中的位置

vertex shader 传给 fragment shader 的inter-stage variable 会针对像素点线性插值

实例化渲染的 instance_index 指的是 draw(v, i)的第二个参数

vertex数据通过storage buffer 传输正在越来越流行

vertex buffer 可以设置step的模式为 vertex 或者 instance

虽然texture本质就是存储颜色的二维数组，但它的特别之处在于通过特殊的硬件 sampler 访问非常高效

texture、sampler等创建之后，还是要放到bindGroup通过它在shader中使用

texture也有好多维度：1d：颜色渐变条；2d：贴图；3d：体积云渲染。通过 texture view 设置

视频纹理使用专门的 texture_external 一个原因是：视频不是用的每个像素点RGBA的方式存储，而是YUV，而且为了压缩比高，YUV不是按像素而是分开存储的

当纹理像素需要缩小时，不能简单的插值，那样会闪烁，需要一种叫mipmap的技术

主要js里不同类型的TypedArray拷贝时是按数字拷贝的，不是按buffer，即[0.9,0.8]会拷成[0,0]，而ArrayBuffer拷贝时是按buffer，因为前者是视图数组。

注意wgsl的struc内存要对齐，一般是4的倍数，最大16

一些常用功能可参见：https://github.com/greggman/webgpu-utils

手动计算偏移量可以在这个网站：https://webgpufundamentals.org/webgpu/lessons/resources/wgsl-offset-computer.html#

注意不透明度还要考虑html的和canvas的，canvas的可在context.configure.alphaMode设置

WebGPU 中任何接受大小或原点坐标的地方，可以是 1 到 3 个数字的数组，或者可以是具有 1 到 3 个属性的对象[1],{x:1,y:2}等

由于映射缓冲区是异步的，从mapAsync到getMappedRange之间时间不确定，解决方法是保持一组始终映射的缓冲区

要注意adapter的限制在不同机器上可能不同，因当只请求必要的限制，并做好异常处理

可通过GPUQuerySet等来监测GPU运行性能，或者chrome的timestamp-query

注意shader执行的时候，index是靠draw的次数定义的，每次输入参数是通过idx*stride来获得的

通过binding数组获取顶点数据更灵活，但attribute获取性能更好，因为它预知了我们是顺序访问的

使用texture最主要的是它内置了采样sample方法，采样的含义是用各种插值方法获取与原数组长度不同的数组

能让fragment shader计算的每个像素点变化的是inter stage variable，它会根据vertex shader输出的每个顶点的inter stage variable进行插值，从而计算出每个像素点的inter stage variable，输入给fragment shader

GPU能够并行运行的精髓就是，它执行次数的index时，并不是对某个数组的顺序迭代，而是通过index*stride取值，这使得先算3后算2结果一样。

point list 仅支持绘制 1px 的点，因为底层api对大像素点的绘制不一致。可自行绘制图形代替点的样式

优化：

- 如果不需要更改缓冲区的数据，用mappedAtCreation: true创建时映射速度会快一些，注意这只影响写入速度

- 应该将顶点的多种数据交错的放在一个数组中，通过步长读取，而不是不同类型放不同数组，因为这样能减少buffer的读写，而且buffer读取连续的快。特别是gltf模型要预处理一下

- 将公用的数据抽取处理放在global uniform buffer中，而不用每个体都带

- 固定的材质等可以放在统一的uniform buffer中，一次初始化，不用每帧都赋值
- 可以采取一个大的uniform buffer，这样写只要一次，然后每个对象的bindgroup用不同偏移量来读取大的buffer，注意uniform buffer偏移量最小值有对齐要求，最小是256
- 使用映射缓冲区而不是读写来优化，由于映射是异步的，一般维护一个映射好的缓冲区数组
- 使用双buffer，因为不能更新当前buffer
- 使用偏移量计算矩阵，即输入大buffer的偏移量就可以开始算，不用创建单个矩阵的视图（当然，这种提升比较小，结合易用性取舍）
- 使用间接绘制pass.drawIndirect
- 使用渲染束render bundle

可以通过device.addEventListener监听shader的异常

只有在特定函数，比如submit执行后才会报出异常

可以用getComplicationInfo获取wgsl错误

debug常用工具：https://github.com/greggman/webgpu-dev-extension

https://github.com/brendan-duncan/webgpu_inspector

空间中总是面向镜头的平面常被称为 billboard 广告牌

控制3d物体转动的常用arcball，它有三个方向：翻滚（roll）、俯仰（pitch）和偏航（yaw）

使用`transferControlToOffscreen`将画布转换为离屏画布，利用webworker来提高渲染性能

并行计算中也采用线程的概念，但和cpu中的线程不同，并行计算中的每个线程程序必须是一样的

工作组缓冲区性能优于存储缓冲区，但只能在同一个工作组内的线程访问到，因此工作缓冲区一般做快速临时存储

shader多线程过程中，可以调用workgroupBarrier()来对齐缓冲区写入

工作组内存被组织成多个bank，如果多个线程访问同一个bank会排队，因此要优化bank冲突

注意workgroup_size一般有256的限制（由maxComputeInvocationsPerWorkgroup决定），因此二维设置为16*16















## WGSL

向量类型如 vec4f 是针对图形场景特化的，有很多方便字段，比如 w, r,g,b,a,s,t,p,q, xy, xyz, rgba 等，甚至可以zzy

数字类型后缀：i, u, f, h，不加的称为AbstractInt和AbstractFloat，表示还没有定下来是哪种

所有变量不管什么前缀都是块级作用域，var 表示有存储的可变量，let是不可变量，const是编译期常量

mix是线性插值

vec是数值类型，全类型的是array

一般的array必须固定size，固定size的array目前不能获得size；当在全局定义，或是struct的最后一个，可以动态size，可通过arrayLength(&foo)获取长度

全局的绑点变量，只有当入口函数调用（或间接调用）到时，才是必须绑定的。同一个文件中多个入口时，使用到的那个入口没用到，也无需绑定

attribute在WebGPU中指vertex attribute，在WGSL中指@XX

@location()用来标定输入输出，vertex shader输入可在结构体定义中标定，形参用结构体或直接是字段都可以；vertex shader和fragment shader之间传递的参数称为 inter state variables，只要location对应就行；对于fragment shader的输出，@location标定GPURenderPassDescriptor.colorAttachment所要接收的。

@builtin()用来标定从WebGPU内置提供的参数（而不是Buffer）来获取或输出

continuting定义继续块，每次迭代（正常或continue）结束下个迭代开始时执行，整个循环结束（正常或break）时不会执行

discard退出shader，只可在fragment shader中使用

断言不需要加括号

没有三元运算符，用select()函数代替

只有a++，没有++a

++，+=只能是语句，不能是表达式

赋值的左边不能是调用

重新调节颜色分量顺序称为swizzle，左侧不能使用swizzle，只能color = vec4(color.bgr, color.a)

当某个变量实际不要用到但语法上用到时，将它赋值给 _

要尽量做边界检查，防止未定义行为

可以使用enable关键字开启实验属性

读取对象和写入对象可用 Src、Dst命名

wgsl文件目前没有引入其它wgsl文件的机制，可以在js中通过文本拼接实现



# 几何

极坐标存在一对多的情况，称为别名（alias）；其中首选的定义一套规则称为规范坐标
