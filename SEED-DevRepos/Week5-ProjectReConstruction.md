# G组项目重构记录-WeekFive

## 前几周整理总结
- 优化、精简每一个脚本的内部和一个模块内部脚本之间的交互逻辑
    - 优化了对象的获取位置--即用即取，确保Unity生命周期不会在Start时过于臃肿
    - 对象的存储与否进行了取舍
    - 判断逻辑优化（&&开关语句优化，枚举配合swtich case实现状态机），属性设置逻辑优化
    - 尽量避免直接操控某一个类的属性，将对应逻辑封装为函数（常表现为reset函数）
    - 整合子类的共性，在父类中添加新逻辑以精简代码（如Life类的移动和实例获取逻辑的优化同时减少了7个子类中的重复代码）
    - 对相机类进行了大量的优化，包括封装镜头过渡行为，提供了新的offset、fov，rotAngle设置函数，修改、优化相对臃肿的逻辑
    - 合并了PlayerMove（钢琴关）和HumanController（游乐场关和天使恶魔关），减少了代码冗余并提高了代码可读性
    - 
- 针对资源获取和使用添加了对象池、资源静态初始化方法--通过享元设计模式优化了对象的复用
- 对所有类的参数和函数名进行了初步的命名优化，重点为状态的函数名修改
- 对一些类的功能实现进行修复（包括WaterCube、MusicStone、MazeController）
- 为了解决脚本移动的时候出现的missing情况，我制作了一个能够遍历GameObject并查找missing or Specific Scrpits的编辑器。功能目前有两种：
        - 根据需要获取一个拥有目标脚本的GameObject的List
        - 为这个List下的Object批量添加或删除特定脚本
在制作完毕之后，发现正确的脚本位置移动方法是.meta与.cs一并剪切到指定位置……
- 添加InputLayer输入控制层，负责处理外部输入的移动逻辑，将外界输入和内部的逻辑处理添加了一层中间层并进行总控，所有可被操控物体的输入都会从InputLayer获取，提高了代码的可维护性和拓展性
- 添加了ScriptableObject制作的FloatReference参数，声明了上下文无关的变量，直接替代了原有的GameManager
- 添加了GameEvent逻辑，相当于增加一层Event Layer以减少Object之间的相互引用，增加了结构上的可拓展性

## 本周整理前关系图
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-seedDev/%E6%95%B4%E7%90%86%E5%89%8D%E5%85%B3%E7%B3%BB%E5%9B%BE.jpg)




## 本周整理总结
-  

## _Camera 相机解耦突破口之一
- 探寻Tweener机制：OnComplete则会清除此前设置的回调，而onComplete可以用于函数回调的叠加。新发现可以使得我们能够基本将Camera的API使用内置了很大一部分，仅有的两个过渡函数可以封装在WorldControl中，完成了Camera与其余脚本的解耦

## CharacterController
- 踩坑：minMoveDistance的设置会导致CharacterController的isGrounded判定出现问题

## 单例模式重构
- 通过MonoSingleTon进行新的单例对象获取模式，增加了一个用于管理单例类的SingletonManager
- 新的单例获取方法能够使得Camera与WorldControl进行解耦
- 确保了以后所有单例类能够得到一个统一的单例创建与使用模式，形成了合适的框架

## WorldControl
- 添加与相机相关的API，使得Camera和Element、Player等需要移动或者镜头过渡的类解耦
- 添加CanvasControl相关的API，将一些需要调用ShowSpecialTip以显示弹窗的类与Canvas模块解耦










