# G组项目重构记录-WeekThree

## Scriptable Object


### 优点
- 把数据真正存储在了资源文件中，管理方式如同其他资源，例如退出运行也一样会保持Object内容的修改
- 可以在项目之间很好的复用，不用再制作Prefab并进行导入导出
- 可以被serialised，自动展示类似MonoBehavior的面板
- 可以自定义新的资源类型来储存我们的数据

### 在CanUFeelMe中的应用
- 用途1：声明上下文无关的全局变量
    - 可以将GameManager中的全局性参数归纳为一个Scriptable Object
    - 替代GameManager，将Player、CanvasController和Ball与GameManager解耦，取而代之的是一个FloatReference类。我们可以通过public拖拽或者是Resource.load的方式使得类与变量HeartFrequency直接关联

- 用途2：制作自己的GameEvent
    - 相当于增加一层Event Layer将Object之间相互的接口调用进行了解耦，增加了结构上的可拓展性---事件的触发将会调用所有已订阅的Listeners的Response函数（观察者模式），这种方式使得我们不需要让事件的触发者去持有目标对象的引用，让大规模的事件回应变得易于管理且易读





