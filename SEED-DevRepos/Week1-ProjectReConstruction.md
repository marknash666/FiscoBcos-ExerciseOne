# G组项目重构记录-WeekOne

## Element

### 命名 
- 修改变量名ifintest为isAffected；修改函数名beforetest为requestAffected;<br/>修改函数名intest为Affected
- 删除无用的时间变量testtime与函数afertest
- 删除Update中无用的时间判断逻辑

### 资源获取
- 增加静态方法Init接口供场景控制脚本调用，静态加载一个Element子类可用的Sphere资源，增强复用性并减少开销
- $\color{#4285f4}{（子类会共享父类的非private静态数据成员）}$

## WorldControl & WorldTwo

### WorldControl增加Awake方法
- WorldControl在Awake中调用Element.Init完成资源初始化
- WorldTwo添加base.Awake()，继承父类通用行为

### WindMill
- 增加bool接口供外界查询风车是否处于旋转状态

### SkyWheel
- 删除冗余的布尔值millisrotate，采用WindMill提供的接口进行逻辑判断
- 对象的查找放在requestAffection中执行，减少游戏场景初始化的开销
- 对象的存储与否进行一定的取舍，逻辑优化

### 2. File Generation  
There are 18 functions for generating configuration files, certification files and keys. We would see them in the following analysis of main(). It is worth mentioning that the function **gen_cert_secp256k1** means using ECC for digital signature and its curve is a standard **secp256k1**, the encryption curve chosen by BitCoin.

### 3. Utilities
1. parse\_ip\_config(): used to parse the IP list file when -f option is enabled
2. getname(): generates a string according to the current path
3. file\_must\_exists(): makes sure that the specified file exist, or the script would stop
4. dir\_must\_exists(): makes sure that the specified directory exist, or the script would stop