# openGL 常用函数及参数的说明 {#汪泽煌}

> \[EAGLContextsetCurrentContext:self.mContext\];

* 设置当前的上下文

> glGenBuffers\(1, &buffer\);

* 创建缓存对象并且返回缓存对象的标示符，第一个参数为需要创建的缓存数量，第二个为用于存储单一ID或多个ID的GLuint变量或数组的地址

> glBindBuffer\(GL\_ARRAY\_BUFFER, buffer\);

* 把缓存对象绑定到GL\_ARRAY\_BUFFER上

> glBufferData\(GL\_ARRAY\_BUFFER,sizeof\(squareVertexData\), squareVertexData,GL\_STATIC\_DRAW\)

* 把顶点数据从CPU内存复制到缓存对象，一般都是拷贝到GPU内存

> glEnableVertexAttribArray\(GLKVertexAttribPosition\);

* 开启对应的顶点属性--数据在GPU端是否可见，即，着色器能否读取到数据，由是否启用了对应的属性决定，这就是glEnableVertexAttribArray的功能

> glVertexAttribPointer\(GLKVertexAttribPosition,3,GL\_FLOAT,GL\_FALSE,sizeof\(GLfloat\) \*5, \(GLfloat\*\)NULL+0\);

* 设置合适的格式以便从buffer中读取数据

* 参数1：指定要修改的顶点属性的索引值

* 参数2：指定每个顶点属性的组件数量。必须为1、2、3或者4。初始值为4。（如position是由3个（x,y,z）组成，而颜色是4个（r,g,b,a））

* > 参数3：指定数组中每个组件的数据类型。可用的符号常量有GL\_BYTE, GL\_UNSIGNED\_BYTE, GL\_SHORT,GL\_UNSIGNED\_SHORT, GL\_FIXED,和GL\_FLOAT，初始值为GL\_FLOAT
* 参数4：指定当被访问时，固定点数据值是否应该被归一化（GL\_TRUE）或者直接转换为固定点值（GL\_FALSE）。

* 参数5：指定连续顶点属性之间的偏移量。如果为0，那么顶点属性会被理解为：它们是紧密排列在一起的。初始值为0。

* 参数6：指定第一个组件在数组的第一个顶点属性中的偏移量。该数组与GL\_ARRAY\_BUFFER绑定，储存于缓冲区中。初始值为0

> CAEAGLLayer

* CAEAGLLayer提供了一个OpenGLES渲染环境。各种各样的OpenGL绘图缓冲的底层可配置项仍然需要你用CAEAGLLayer完成，它是CALayer的一个子类，用来显示任意的OpenGL图形。OpenGL由近350个不同的函数调用组成，用来从简单的图元绘制复杂的三维景象，主要用途是CAD、科学可视化程序、虚拟现实、游戏程序设计。

> CAEAGLLayer的属性 ：drawableProperties ，直接将设置放在字典中赋值即可
>
> self.myEagLayer.drawableProperties= \[NSDictionarydictionaryWithObjectsAndKeys:
>
> \[NSNumbernumberWithBool:NO\],kEAGLDrawablePropertyRetainedBacking,kEAGLColorFormatRGBA8,kEAGLDrawablePropertyColorFormat,nil\];

* kEAGLDrawablePropertyRetainedBacking--为FALSE，表示不想保持呈现的内容，因此在下一次呈现时，应用程序必须完全重绘一次，将该设置为TRUE对性能和资源影像较大，因此只有当renderbuffer需要保持其内容不变时，我们才设置为TRUE

* kEAGLDrawablePropertyColorFormat--颜色格式，枚举值

> \[self.myContextrenderbufferStorage:GL\_RENDERBUFFERfromDrawable:self.myEagLayer\];

* 为颜色缓冲区分配存储空间

> 以下为透视相关操作函数
>
> GLuint projectionMatrixSlot =glGetUniformLocation\(self.myProgram,"projectionMatrix"\);//获取着色器程序中,指定为uniform类型变量的id，也就是获取透视矩阵（projectionMatrix表示是透视矩阵）的下标位置
>
> KSMatrix4\_projectionMatrix;
>
> ksMatrixLoadIdentity\(&\_projectionMatrix\);//生成透视矩阵
>
> ksPerspective\(&\_projectionMatrix,30.0, aspect,5.0f,20.0f\);//透视变换，视角30°，5个参数的意义：result矩阵，视角，长宽比，近平面距离，远平面距离。
>
> //设置glsl里面的投影矩阵
>
> glUniformMatrix4fv\(projectionMatrixSlot,1,GL\_FALSE, \(GLfloat\*\)&\_projectionMatrix.m\[0\]\[0\]\);//调用glUniformMatrix4fv这个函数，将矩阵传递到Shader中。它的参数分别为：下标位置，矩阵数量，是否进行转置，矩阵
>
> glEnable\(GL\_CULL\_FACE\);//开启剔除操作效果,glCullFace指明多边形的前面或后面是否被剔除
>
> * 
> ksMatrixMultiply\(&\_modelViewMatrix, &\_rotationMatrix, &\_modelViewMatrix\)

* 把变换矩阵相乘，注意先后顺序



