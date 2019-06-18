# LAGCredit合约的编译、部署、SDK开发

## 目标：通过SpringBoot完成对LAGCredit合约的编译、部署与SDK开发

**官方文档**

># Spring Boot Starter
>### 运行
>编译并运行测试案例，在项目根目录下运行：
>```
>$ ./gradlew build
>```
>当所有测试案例运行成功，则代表区块链运行正常，该项目通过SDK连接区块链正常。开发者可以基于该项目进行具体应用开发。

## gradlew build
运行官方提供的测试用例，确保当前项目可以用于应用开发
### 在学校电脑上的build
我选择配置的java环境为1.8.0_211
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/java_env.png)

build比较成功，且没有warning或error
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/gradlew_build.png)
### 在提供的virtualbox环境下的build
虚拟机用的是openjdk 11.0.3版本
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/gradlew_build_virtual.png)

build虽然成功，但是出现了error和warning
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/gradlew_build_virtual.png)

## 
