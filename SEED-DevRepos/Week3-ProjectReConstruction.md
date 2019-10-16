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


s