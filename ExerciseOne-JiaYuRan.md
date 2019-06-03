
## 1. 查看区块高度
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/1.png?raw=true)
通过getBlockNumber得到区块的高度

## 2. 部署HelloWorld智能合约
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/2.png?raw=true)
通过deploy指令部署并获取合约地址

## 3. 使用查看getDeployLog
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/3.png?raw=true)
部署信息可以通过getDeployLog获取

## 4. 获取区块数据
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/5.png?raw=true)

## 5. 查看区块高度
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/4.png?raw=true)
再次通过getBlockNumber获取区块高度，发现部署之后区块高度增加了1

## 6. 调用智能合约
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/6.png?raw=true)
调用set设置name变量 此处的合约地址是deploy指令返回的地址

## 7. 再次查看区块高度
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/7.png?raw=true)
再次通过getBlockNumber获取区块高度，发现部署之后区块高度增加了1

## 8. 获取区块数据
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/8.png?raw=true)

## 9. 按照CNS方式部署HelloWorld智能合约
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/9.png?raw=true)
通过deployByCNS + contract_name + version 即可以CNS方式部署合约

## 10. 再次查看区块高度
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/10.png?raw=true)
再次通过getBlockNumber获取区块高度，可以发现进行CNS部署之后区块高度增加了2

## 11. 获取区块数据
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/11.png?raw=true)




