# LAGCredit在SpringBoot环境下的接口开发
### JSON依赖添加
```
compile 'net.sf.json-lib:json-lib:2.4:jdk15'
```
加入依赖后IDEA会自动下载包括FastJSON在内的jar包。在实际使用时，需要注意的是fastjson和net.sf.json的JSONObject的String转换方法有区别（前者为toJSONString,后者则是简单的toString。

## 接口开发

### 合约部署
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/interface_dev2.png)

### 积分传输
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/interface_dev1.png)

![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/interface_dev3.png)

### 当前积分查看
![](https://github.com/marknash666/FiscoBcos-Exercises/blob/master/images/image-for-springboot/interface_dev4.png)

