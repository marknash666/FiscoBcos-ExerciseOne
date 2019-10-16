# G组项目重构记录-WeekThree

## MazeController
- 修改resetBool函数为resetMaze，添加位置重置逻辑

## FireBallon
- 修改resetSpeed函数为resetBallon，添加位置重置逻辑

## WorldTwo 
- 将迷宫的重置职责封装在MazeController中，简化逻辑
- 将热气球位置逻辑重置逻辑封装在热气球reset函数中，简化逻辑

## Piano 
- 钢琴被影响的逻辑进行合并

## WorldOne
- 本关中，看向云朵的镜头逻辑比较特殊，假如要使用现有函数则需要创建两个空物体，实际上不如直接操作transform来得简单明了。待定
- 将镜头、人物等限制逻辑换成对应的接口

## CameraTrigger
- 将镜头转移逻辑用对应接口重写

## PeopleControl 
- 将心跳波Sphere同样改为静态加载
- 更改了beforeControl的调用位置，更好理解
--------------------------
## WorldPlot 
- 更新createdialog、delete的判断逻辑，简化代码
- 删除无用的create函数

## TipCube 
- 精简了几乎所有代码，将之前的冗余代码逻辑归并至CanvasControl，使得代码更加简洁明了易读

## CanvasControl
- 重构了弹窗计数的逻辑
- 添加了numsofTips代码供外部调用，弹出对应数量的提示
- 优化了代码的判断逻辑

## PeopleControl
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-seedDev/Main.jpg)
- 实际上，在本游戏的设计中，可操控物体的状态转移图可以概括为上图。据此，设计了两种请求函数和两个退出函数供状态转移使用

## BirdTwo
- 将原有的布尔值controlPlayer和cancontrol改为枚举类型Idle，Transition,Controlled,PlayerCaught，使得逻辑更加清晰
- 去掉了keepPlayer函数吗，使得控制逻辑全部在beingControl中通过枚举配合switch case实现状态机

## Horse
- 将触发鸟笼开启的一系列写成操作转移到世界控制脚本中，对Horse与相关脚本进行合理的解耦
- 添加音乐播放函数接口

## InputLayer
- 添加输入控制层，负责处理外部输入的移动逻辑，将外界输入和内部的逻辑处理添加了一层中间层并进行总控，提高了代码的可维护性和拓展性:封装了Input.GetAxis,Input.GeyKey,Input.GetKeyDown等函数
- 所有可被操控物体的移动输入都会从InputLayer的getMovementInput函数中获取，其余跳跃和交互则可调用getJumpState，getInteractionState



