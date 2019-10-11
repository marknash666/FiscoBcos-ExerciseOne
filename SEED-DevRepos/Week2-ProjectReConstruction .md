# G组项目重构记录-WeekTwo

## PeopleControl

- 优化状态函数命名为：ControlRequest,beingControlled,WithDrawal
- 采用_Camera提供的新的镜头过渡接口，优化逻辑
- 利用对象池重写心跳波的实例化

## _Camera 唯一镜头控制类
- changeCenterPoint函数逻辑修改，仅提供摄像机中心位置修改的功能（Update：函数逻辑直接合并入过度函数，本函数仅供世界脚本WorldTwo调用）
- 添加两种过度函数，分别提供过渡到相机和过渡到某一个特定的对象;在功能与参数获取上两个函数有较大差异
- 增加一个新的三维向量以储存过渡到相机之前offset状态
- 根据新增逻辑修改PeopleControl等脚本中的镜头过渡方法
- 调整original_offset逻辑，使得镜头过渡效果正常
- 考虑到迷宫与玩家所需的视角限制的不同，增加RotAngle设置函数
- 增加了一个GameObject作为camForward时的中心点
- 删除了原有的、相对臃肿的过度逻辑，精简了代码
- 对镜头过度代码进行细节调整以达到合适的镜头移动表现形式
- 将重复代码分离成单独的函数


## CameraRotate 
- 删除本脚的大量职责，仅剩一个位置重置函数（Update：函数逻辑已全部无用）

## WorldTwo
- 根据新的镜头offset逻辑增加相关的重置代码
--------------------------------------------------------------------------
## HumanController
- 重命名FixedDisplacement为restrictMovement,将位移逻辑分离出来放入displacement函数中
- FixedDisplacement添加重力开关

## Player
- 优化状态函数命名为：ControlRequest,beingControlled,Release和布尔值命名
- 赋予某些函数以更加”信雅达“的命名
- 采用_Camera提供的新的镜头过渡接口，优化逻辑

## WorldTwo 
- 根据新的相机代码调整revive函数代码，确保相机的正确表现

## MusicCube
- 优化布尔值命名

## LastCube
- 优化实例获取逻辑、布尔值命名

## PeopleControl
- 新增CharacterMovement函数作为基本的对象移动函数
- 整合了子类的一部分移动、实例获取逻辑，精简代码（同时减少了7个子类中的重复代码）

## BirdTwo
- 利用对象池重写心跳波的实例化