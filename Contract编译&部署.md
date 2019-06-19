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
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/gradlew_build1.png)
### 在提供的virtualbox环境下的build
虚拟机用的是openjdk 11.0.3版本
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/gradlew_build_virtual.png)

build虽然成功，但是出现了error和warning
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/gradlew_build_virtual.png)

## 合约编译
**本次编译运行环境为IntelliJ IDEA**

**官方文档**
># Spring Boot Starter
>### Solidity合约文件转Java合约文件测试
>提供SolidityFunctionWrapperGeneratorTest测试类测试Solidity合约文件转Java合约文件。
><br/>........<br/>
>该测试案例将src/test/resources/contract目录下的所有Solidity合约文件(默认提供HelloWorld合约)均转为相应的abi和bin文件，保存在src/test/resources/solidity目录下。然后将abi文件和对应的bin文件组合转换为Java合约文件，保存在src/test/java/org/fisco/bcos/temp目录下。SDK将利用Java合约文件进行合约部署与调用。

1. 将LAGCredit.sol放到spring-boot-starter/scr/test/resources/contract目录下
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/compile_1.png)
2. 然后运行官方提供的Solidity合约文件转Java合约文件测试类
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/contract_2.png)
3. 成功的话，我们可以在spring-boot-starter/src/test/java/org/fisco/bcos/temp目录下得到LAGCredit.java，然后将其拷贝到main目录下供开发使用
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/contract_3.png)

## LAGCreditController开发与功能验证
根据老师提供的实验pdf开始LAGCreditController类的编写

### 遇到的问题
为了验证Controller的功能正确性，我便写了LAGCreditTest JUint测试类来对控制器的功能进行测试。其中，发现在Test类中deploy，load等函数都是无法正常执行的。