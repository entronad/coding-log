WebGPU的坐标系称为标准设备坐标系（NDC）是现代图形接口都采用的坐标空间；vertex shader output 的输出空间会被gpu裁剪到屏幕范围内，所以也被称为 clip space，坐标后面再添个1称为齐次坐标，vertex shader output也被称为齐次空间

贴图分三种：图像贴图，canvas贴图，video贴图，注意video贴图各方面都很不一样

多物体资源绑定有四种方法：buffers, buffer with offsets, dynamic offsets, instance

贴图可以使用一些更高效的新格式：webp, webp2, jpeg xl, avif

视频贴图可使用更高效的贴图：vp8/9, av1

可以用顶点索引制定三角，类似triangle-strip的压缩数据，但还是triangle-list模式

为了灵活，一般modelView矩阵和project矩阵是分别传入shader中在里面再组成mvp矩阵，以便与Camara矩阵分别处理

注意shader虽然是GPU计算，但它会被执行多次，所以不能指望太多东西在shader中计算，尽量在外面算好

由于mapAsnc的效率很低，所以要尽量减少GPU和CPU同步缓冲区的次数，可通过bindGroup在不同的管线中直接共享

多个管线串联中间只要end，最后encoder只submit一次