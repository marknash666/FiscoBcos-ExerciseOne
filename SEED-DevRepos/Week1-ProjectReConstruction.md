# G组项目重构记录-WeekOne

## Element & 子类
### 命名优化
- 修改变量名ifintest为isAffected；修改函数名beforetest为requestAffected;<br/>修改函数名intest为Affected
- 删除无用的时间变量testtime与函数afertest
- 删除Update中无用的时间判断逻辑

### 资源获取
- 增加静态方法Init接口供场景控制脚本调用，静态加载一个Element子类可用的Sphere资源，增强复用性并减少开销
PS:子类会共享父类的非private静态数据成员

## WorldControl & WorldTwo
- WorldControl在Awake中调用Element.Init完成资源初始化
- WorldTwo添加base.Awake()，继承父类通用行为

## WindMill
- 增加bool接口供外界查询风车是否处于旋转状态
- 变量名优化，布尔值canrotate改为isRotate

## SkyWheel
- 删除冗余的布尔值millisrotate，采用WindMill提供的接口进行逻辑判断
- 对象的查找放在requestAffection中执行，减少游戏场景初始化的开销
- 对象的存储与否进行一定的取舍，逻辑优化

## PeopleControll & 子类
### 命名优化
- 枚举类型enter改为Controlled;枚举类型tested改为Affected
- 大量函数名修改

## 脚本寻找编辑器
- 为了解决脚本移动的时候出现的missing情况，我制作了一个能够遍历GameObject并查找missing or Specific Scrpits的编辑器
- 功能目前有两种：
    - 根据需要获取一个拥有目标脚本的GameObject的List
    - 为这个List下的Object批量添加或删除特定脚本
- 在制作的过程中，发现正确的脚本位置移动方法是meta与cs一并**剪切**到指定位置
-----------------------------------------

## RockCube

- 布尔值ischange改为isChanged
- 增加了双协程形式实现的的方块消失与位移

## WaterCube
- 分离OnTriggerStay中的`transform.Find("top").gameObject.SetActive(false)`与“玩家GameObject的查找、存储”等逻辑至OnTriggerEnter; 将OnTriggerStay原有的船与人物控制代码改为调用相应的接口
- 增加冰块化水时间的变量（原为硬编码）
- 去除了无用的布尔值noeffect，修改&&判断的顺序，减少判断开销
- 增加数据成员以存储特定的Component组件，减少GetComponent的额外开销


## HumanController
- 为了限制人物移动，此前采用的是直接设置`GetComponent<HumanController>().enabled`.为了增加代码的优雅程度并解耦，增加了布尔值m_Movable与FixedMovement固定位移函数

## Boat
- 新增displacement函数，处理位移逻辑