# opengl\_知识点03（frame Buffer 和 render Buffer） {#wangzwangzewangzehwangzehuwangzehuawangzehuanwangzehuang汪泽煌}

buffer分为frame buffer和render buffer两大类，其中frame buffer相当于render buffer的管理者，frame buffer object即称为FBO，常用于做离屏渲染缓冲等。render buffer则又可分为三类，color buffer / depth buffer / stencil buffer。

* [ ] 1.生成frame buffer object的API函数：

* glGenFramebuffers\(1, &framebuffer\);

* glBindFramebuffer\(GL\_FRAMEBUFFER, framebuffer\);

生成render buffer的API函数，render buffer的生成函数是一样的，buffer句柄类型只有在进行分配buffer空间的时候才会确定：

* glGenRenderbuffers\(1, &renderbuffer\);

* glBindRenderbuffer\(GL\_RENDERBUFFER, renderbuffer\);2.

* [ ] 2.frame buffer仅仅是管理者，不需要分配空间；render buffer的存储空间的分配，对于不同的render buffer，使用不同的API进行分配，而只有分配空间的时候，render buffer句柄才确定其类型

* \(1\).最基本的是color buffer，调用EGALContext的OC方法为其分配空间

> * \(BOOL\)renderbufferStorage:\(NSUInteger\)target fromDrawable:\(id&lt;EAGLDrawable&gt;\)drawable;

* \(2\).而depth buffer则可以直接调用openGL本身的API进行分配

> glRenderbufferStorage\(GL\_RENDERBUFFER,GL\_DEPTH\_COMPONENT16, width, height\);

* [ ] 3.上面\(1\)\(2\)函数是用于生成render buffer的存储空间，生成空间之后，则需要将renderbuffer跟framebuffer进行绑定，调用glFramebufferRenderbuffer函数进行绑定，后面的绘制才能起作用

* [ ] 4.接下来可以调用OpenGL的函数进行绘制处理，最后则需要调用EGALContext的OC方法进行最终的渲染绘制，这里渲染的是color buffer，这个方法会讲buffer渲染到CALayer上面

> * \(BOOL\)presentRenderbuffer:\(NSUInteger\)target;

* [ ] 5.还有一个需要注意的地方是在退出的时候，需要调用glDelegateFramebuffers或者glDeleteRenderbuffers函数删除frame buffer或者render buffer



