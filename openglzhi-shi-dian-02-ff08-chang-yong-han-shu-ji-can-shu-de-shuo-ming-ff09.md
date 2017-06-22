# openGL 常用函数及参数的说明



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



