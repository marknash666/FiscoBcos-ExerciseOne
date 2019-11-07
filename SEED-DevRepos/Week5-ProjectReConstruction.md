# G组项目重构记录-WeekFive

## 前几周整理总结
- 重点优化在每一个脚本的内部和一个模块内部脚本之间的交互逻辑
 - 优化了对象的获取位置--即用即取，确保Unity生命周期不会在Start时过于臃肿
 - 对象的存储与否进行了取舍
 - 
- 针对资源获取和使用添加了对象池、资源静态初始化方法--通过享元设计模式优化了对象的复用
- 对所有类进行了初步的命名优化
- 为了解决脚本移动的时候出现的missing情况，我制作了一个能够遍历GameObject并查找missing or Specific Scrpits的编辑器
 - 功能目前有两种：
根据需要获取一个拥有目标脚本的GameObject的List
为这个List下的Object批量添加或删除特定脚本



## _Camera
- 探寻Tweener机制：OnComplete则会清除此前设置的回调，而onComplete可以用于函数回调的叠加。新发现可以使得我们能够基本将Camera的API使用内置了很大一部分，仅有的两个过渡函数可以封装在WorldControl中，完成了Camera与其余脚本的解耦
- 踩坑minMoveDistance的设置会导致CharacterController的isGrounded判定出现问题

## 单例模式重构
- 通过MonoSingleTon进行新的单例对象获取模式，增加了一个用于管理单例类的SingletonManager
- 新的单例获取方法能够使得Camera与WorldControl进行解耦
- 确保了以后所有单例类能够得到一个统一的单例创建与使用模式，形成了合适的框架

## WorldControl
- 添加与相机相关的API，使得Camera和Element、Player等需要移动或者镜头过渡的类解耦
- 添加CanvasControl相关的API，将一些需要调用ShowSpecialTip以显示弹窗的类与Canvas模块解耦










