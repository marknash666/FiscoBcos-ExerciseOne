# G组项目重构记录-WeekThree

## Scriptable Object
### 优点
- 把数据真正存储在了资源文件中，管理方式如同其他资源，例如退出运行也一样会保持Object内容的修改
- 可以在项目之间很好的复用，不用再制作Prefab并进行导入导出
- 可以被serialised，自动展示类似MonoBehavior的面板
- 可以自定义新的资源类型来储存我们的数据

### 在CanUFeelMe中的应用
- 可以将GameManager中的全局性参数归纳为一个Scriptable Object
- 替代GameManager，将Player、CanvasController和Ball与GameManager解耦，取而代之的是一个FloatReference类。我们可以通过public拖拽或者是Resource.load的方式使得类与变量HeartFrequency直接关联





