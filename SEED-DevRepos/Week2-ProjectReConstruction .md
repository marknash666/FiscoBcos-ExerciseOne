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

--------------------------------------------------------------------------
## HumanController
- 重命名FixedDisplacement为restrictMovement,将位移逻辑分离出来放入displacement函数中
- FixedDisplacement添加重力开关参数

## Player
- 优化状态函数命名为：ControlRequest,beingControlled,Release和布尔值命名
- 赋予某些函数以更加”信雅达“的命名
- 采用_Camera提供的新的镜头过渡接口，优化逻辑

## WorldTwo 
- 根据新的相机代码调整revive函数代码，确保相机的正确表现
- 根据新的镜头offset逻辑增加相关的重置代码

## MusicCube
- 优化布尔值命名

## LastCube
- 优化实例获取逻辑、布尔值命名

## PeopleControl
- 新增CharacterMovement函数作为基本的对象移动函数
- 整合了子类的一部分移动、实例获取逻辑，精简代码（同时减少了7个子类中的重复代码）

## BirdTwo
- 利用对象池重写心跳波的实例化

## MusicStone
- 将material的rendering mode改为Fade，修复了云的表现形式（渐隐渐显）
- 更正materialRenderer的开启和关闭逻辑

## FadeCube 
- 精简逻辑

## Slide 
- 优化实例获取逻辑
- 更新人物移动限制逻辑
- 优化人物滑落的表现形式

## Ball 
- 优化“限制心跳波一次影响多个物体”的逻辑，修改布尔值命名
- 优化脚本获取逻辑

----------------------------------------------------------
## HumanController （与 PlayerMove合并）
- 将HumanController改用Character Controller控制浮空逻辑
- Character Controller 的 isGrounded 判断需要我们给予模型一点y轴负方向的位移以确保模型与地面的贴合（大量调试工作）
- m_Movement逻辑优化
- 优化掉落逻辑
- 踩坑记录：
    - 需要将玩家瞬移时应先disable Character Controller 
    - 此前，TriggerTest脚本的OnTriggerEnter与玩家自身用于判断是否在地面上的Trigger是冲突的，造成实现效果非常差；引入Character Controller后，可以将玩家自身的Trigger删除，贴片复活脚本的功能能满足现实

## WaterCube 
- 增加水块与船的距离判断逻辑，拉大了船身，极大地优化了船的表现形式
- 通过HumanController的优化改善了玩家从船上掉落的表现形式
- 修复了场景的一些bug

## _Camera
- 增加offset存储函数saveOffset，确保复活时镜头的正确表现形式

