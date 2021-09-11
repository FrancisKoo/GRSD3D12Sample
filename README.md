# Gamebaby Rock Sun's D3D12 C-Style Sample Code for beginner

&emsp;&emsp;整个项目使用VS2019构建，请自行安装VS2019打开sln文件。

&emsp;&emsp;关于这些示例的详细讲解请到我的CSDN博客查看： https://blog.csdn.net/u014038143 

&emsp;&emsp;教程中的代码跟现在这个项目中的代码有些出入，示例代码请以这里为准。

&emsp;&emsp;这套示例代码的目标就是不使用任何封装，并且使用比较原始的C-风格代码来展示D3D12编程的方方面面。不使用任何封装使大家更集中精力于D3D12本身，而不至于分散注意力。并且线性化（甚至连独立的函数都没有怎么封装）的代码风格有助于大家学习和理解D3D12，根本目的就在于让大家彻底理解和消化D3D12本身。当彻底搞明白D3D12接口之后，各位想怎么封装就怎么去封装吧。那才是真正的自由王国！

# 1、1-D3D12Triangle

&emsp;&emsp;这个例子相当于Hello World，只是简单的绘制一个三角形出来；

![1](ScreenShot/image-20191212130745840.jpg)

# 2、2-D3D12WICTexture

&emsp;&emsp;这个例子演示如何使用WIC加载一个图片纹理，重点在于搞明白D3D12中的纹理加载的过程，理解“两次Copy”操作的基本过程（请注意代码中的注释说明），这是理解D3D12资源加载的基础。

![2](ScreenShot/image-20191212131202059.jpg)

# 3、3-PlacedTexture

&emsp;&emsp;这个示例效果上与第二个示例一样，该示例中主要展示的是使用D3D12中的Placed（定位方式）的Texture，重点在于自建显存堆/共享内存堆的创建和使用上。

![image-20191212143219661](ScreenShot/image-20191212143219661.jpg)

# 4、4-D3D12TextureCube

&emsp;&emsp;这个例子主要展示DirectXMath库基本操作方法、使用独立堆创建常量缓冲、理解管线状态对象、理解围栏同步等内容，并且开始绘制一个真正的3D立方体。

![image-20191212144339456](ScreenShot/image-20191212144339456.jpg)

# 5、5-SkyBox

&emsp;&emsp;这个例子主要让大家学会使用和理解捆绑包，并且开始学会加载并使用DDS Cube Map。

![image-20191212144604816](ScreenShot/image-20191212144604816.jpg)

# 6、6-MultiThread

&emsp;&emsp;这个示例是比较重要的一个例子，展示了如何进行多线程渲染，本质上就是使用多个线程和多个CommandList来记录渲染命令。这个例子只是简单的搭起了一个多线程渲染的基本框架而已，这种简单性的目的就是方便大家彻底掌握多线程渲染。

![image-20191212144926221](ScreenShot/image-20191212144926221.jpg)

# 7、7-D3D12MultiAdapter

&emsp;&emsp;这个示例主要展示如何充分利用系统中的多个显卡来进行渲染，主要是演示异构多显卡渲染，比较典型的可以应用于有独显及核显的笔记本系统，这样的系统比较常见。核心就是跨显卡共享纹理，不能共享纹理，最差也能够共享缓冲Buffer，这是D3D12的基本要求。

![image-20191212164234428](ScreenShot/image-20191212164234428.jpg)

# 8、8-UIRenderBase

&emsp;&emsp;这个示例主要演示了基本的UI渲染图片的正交投影变换矩阵的生成，图片的Alpha Blend 显示，以及基本的划线操作等。

![image-20191212164530404](ScreenShot/image-20191212164530404.jpg)

# 9、9-D3D12RenderToTexture

&emsp;&emsp;这个示例主要展示在D3D12中如何渲染到纹理。渲染到纹理是很重要的一个方法，是很多渲染特效需要的基本功能。

![image-20191212164743263](ScreenShot/image-20191212164743263.jpg)

# 10、10-PixelShaderTips

&emsp;&emsp;这个示例主要演示了一些很古老的仿照Photoshop中的滤镜效果的Pixel Shader在D3D12中的实现。其中的方法都还没有优化，只是做到了将公式直接翻译成Shader的工作。

![image-20191212165443030](ScreenShot/image-20191212165443030.jpg)

![image-20191212165524944](ScreenShot/image-20191212165524944.jpg)

# 11、11-MultiThreadAndAdapter

&emsp;&emsp;这个示例主要为了在前一个例子基础上正确实现水彩画效果，需要后渲染的高斯模糊处理，同时该示例主要展示了多线程+多显卡渲染的基本方法，并且将高斯模糊后处理主要丢到了辅助显卡上去执行。同时该示例中的高斯模糊就是经典的两遍渲染来实现了，效率上比前一个例子中的“九宫格”方式的实现高了近50%，GPU占用从40%-50%降到了20%左右。

![image-20191212180600560](ScreenShot/image-20191212180600560.jpg)

# 12、12-D2DWriteOnD3D12

&emsp;&emsp;这个示例主要展示在多线程多显卡渲染架构的基础上再融入D2D和DWrite，这样方便显示一些文字信息，为性能考虑有意将D2D和DWrite放在了辅助显卡（一般是核显）上来执行，这样主显卡就专心去做渲染的工作。

![image-20191213145910521](ScreenShot/image-20191213145910521.jpg)

# 13、13-ShowGIFAndResourceStatus

&emsp;&emsp;这个示例主要展示如何使用WIC加载GIF动画图片，同时当做纹理来显示。GIF动画的处理主要使用到了Direct Computer作为预处理管线。重点就是展示使用Direct Computer来做纹理图片的预处理的技术，这是一个很重要的基本技巧。这个例子由将基本框架回复到了单线程单显卡渲染的基础上。重点是演示现代显卡的多引擎架构，即有3D引擎、计算引擎，可以同时创建多个分别代表这些引擎的命令队列，并演示了多个引擎间同步的方法。

![image-20191213150308181](ScreenShot/image-20191213150308181.jpg)

# 14、14-MultiThreadShadow

&emsp;&emsp;该示例主要展示使用多线程渲染时，如何进行多线程多Pass组合渲染来显示阴影。其中的渲染到深度缓冲的方法是一个十分重要的方法，是现代比较流行的延迟渲染、Forward+等渲染技术的核心基础技术之一。（该示例还在开发中，完成后提交并进一步补充文档及运行截屏）。

# 15、15-CPUThreadsBarrier

&emsp;&emsp;该示例是一个纯的只使用了命令行的用于演示“3个内核同步对象实现渲染线程池/大规模线程池”的例子代码，为了大家能够掌握这种专门的用于渲染线程池的框架原理，这个示例中把所有真实的D3D12渲染的代码都删除掉了，只是保留了简单的命令行输出提示，代表插入真实渲染代码的位置。运行后的效果如下：

![image-20210602175020698](ScreenShot/image-20210602175020698.jpg)

# 16-Assimp_Data_Display

&emsp;&emsp;该示例基于命令行格式化的显示了Assimp导入模型的数据及数据结构，让大家先对模型数据有一个感性的认识，好进一步掌握3D骨骼动画的原理及运用方法。

![image-20210604111201535](ScreenShot/image-20210604111201535.jpg)

# 17-D3D12_Assimp_Animation

&emsp;&emsp;该示例展示了使用Assimp导入动画文件，并用基本的D3D12渲染框架渲染，还没有加任何的光照效果，只是简单的展示3D骨骼动画的基本原理。

![16233246465942021610193211](ScreenShot/16233246465942021610193211.gif)

# 18-PBR-Base-Point-Lights

&emsp;&emsp;该示例展示基础的PBR渲染过程，重点在PS_PBR_Base_Point_Lights.hlsl文件中。基于物理的渲染（PBR）是现代渲染的主流技术，与传统光照纯几何式的光照渲染方式已经大相径庭，本系列示例即直接跳过传统光照，直接进入现代化的PBR渲染的学习与展示。本例中用了8个点光源，照明了一个球体，使用了PBR中比较流行的“金属工作流”渲染模型，即主要材质参数是金属度、粗糙度、反射率等，其中反射率模拟了8种金属，可以使用Tab键切换反射率，用A、Q键对-控制金属度、W、E键对-控制粗糙度、E、D键对-控制环境遮挡系数。由于使用的是点光源，这个示例在纯金属最低粗糙度时，仅有高光点，这其实是不对的。例子的真实目的是给大家展示基本的PBR光照方程变成代码的样子。最终需要注意的是，学习D3D12接口编程的终极目的是掌握现代渲染算法和技术，因此后续的例子都希望大家对前面各个例子中的一些D3D12基本操作都有了牢固的掌握，或者说D3D12本身不应再成为大家学习的障碍，而是一个有力的工具！如果前序例子还有疑问或者我可能没有交代清楚的细节，大家都可以随时到本人博客：[Gamebaby Rock Sun的博客](https://blog.csdn.net/u014038143?spm=1000.2115.3001.5343) 留言提问。本示例运行效果截图如下（一个略显粗糙的金色金属球，可以通过按键调整至此效果）：

![image-20210627151630910](ScreenShot/18.png)

# 22-MultiInstance-PBR-Sphere

&emsp;&emsp;这个示例是18号示例的自然延续，使用了多实例技术来呈现PBR的球体阵列，可以更加直观的看到金属流形式的虚拟物理参数对PBR效果细腻的影响。效果如下：

![image-20210911203050730](ScreenShot/22.jpg)

