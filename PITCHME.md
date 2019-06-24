<<<<<<< HEAD
# LAGCredit合约阅读分析与功能添加
+++
## 代码分析
+++
1. 数据、事件定义
```solidity
string name = "LAGC";//默认积分名称
string symbol = "LAG";//默认积分代号
uint256 totalSupply;//积分总量
mapping (address => uint256) private balances;//记录账号持有积分数目的结构体(key为address，value为uint256)
event transferEvent(address from, address to,uint256 value);//定义了一个名为transferEvent的事件，该事件会被Web3.js监听并作出响应
=======
# Lab-One Illustration of Build_Chain.sh 

## Function Classification
There are 38 functions in total. Mainly, we could distribute them into 5 classes.
### 1. Information Display 
1. help(): Prints the help information 
2. LOG_WARN(): Prints the warnings
3. LOG_INFO(): Prints the normal information
4. fail_message(): Prints the fail message
+++
### 2. File Generation  
There are 18 functions for generating configuration files, certification files and keys. We would see them in the following analysis of main(). It is worth mentioning that the function **gen_cert_secp256k1** means using ECC for digital signature and its curve is a standard **secp256k1**, the encryption curve chosen by BitCoin.
+++
### 3. Utilities
1. parse\_ip\_config(): used to parse the IP list file when -f option is enabled
2. getname(): generates a string according to the current path
3. file\_must\_exists(): makes sure that the specified file exist, or the script would stop
4. dir\_must\_exists(): makes sure that the specified directory exist, or the script would stop
5. dir\_must\_not\_exists(): makes sure that the specified file do not exist, or the script would stop
6. check\_and_install\_tassl(): installs the tassl if it does not exist
7. check\_name(): ensure that the string do not have any character except ^[a-zA-Z0-9._-]+$
+++
### 4.Implementation body
The last four row of code shown below are the functions called during the actual implementation of the shell file.
>>>>>>> a06309d6a5943cb12da540b7bf86ffbd6e85be4e
```
+++
2. 构造函数
```solidity
constructor (uint256 initialSupply, string creditName,string creditSymbol) public{
        totalSupply =initialSupply;//初始化积分总量
        balances[msg.sender]=totalSupply;//初始化合约持有者的积分数
        name=creditName;//初始化积分名称
        symbol=creditSymbol;//初始化积分代号        
    }
```
+++
<<<<<<< HEAD
3. getTotalSupply
```solidity
function getTotalSupply() view public returns (uint256){
        return totalSupply;//用于查看当前积分总量的函数
    }
=======
### Part One - check_env()
>>>>>>> a06309d6a5943cb12da540b7bf86ffbd6e85be4e
```
+++
4. _transfer(internal的传递执行体)
```solidity
function _transfer(address _from,address _to,uint _value) internal{        
        require(!(_to == 0x0));//防止积分被送进焚烧地址
        require(balances[_from]>=_value);//确保执行者拥有的积分大于传递的积分数值
        require(balances[_to]+_value > balances[_to]);//确保传递的积分数值大于0
        
        uint previousBalances = balances[_from]+ balances[_to];//记录传递执行前两个账户的积分总额
        
        balances[_from] -= _value;//积分送出者积分减少
        balances[_to] += _value;//积分获得者积分增加
        
        emit transferEvent(_from,_to,_value);//激活积分传递事件
        assert(balances[_from]+balances[_to] == previousBalances);//假如传递执行后两个帐户的积分总额与此前不一则出现重大错误，回滚        
    }
```
<<<<<<< HEAD
+++
5. transfer(封装了内部执行的积分传递函数)
```solidity
function transfer(address _to, uint256 _value) public {
        _transfer(msg.sender,_to,_value);//将调用者的地址并与其余两个参数传给实际执行体
    }
```
+++
6. balanceOf
```solidity
 function balanceOf(address _owner) view public returns(uint256){
        return balances[_owner];//查看传入地址所拥有的积分数
    }
```
+++
## 功能添加
+++
1. 积分总量增加</br>
**构思：积分总量的添加只能由合约持有者进行操作，因此考虑增加修饰函数和一个储存合约持有者地址的数据，在执行添加操作前判断是否为合约持有者**</br>
+++
**具体实现：**</br>

以下是新增加的代码
```solidity
address contract_holder;//储存合约持有者的地址

modifier onlyOwner(address){
        require(msg.sender==contract_holder);//只能合约持有者进行操作的修饰函数
        _;
    }

function addSupply(uint256 amountofSupply) public onlyOwner(msg.sender) {
        totalSupply= amountofSupply+totalSupply;//修改积分发放总量
        balances[msg.sender] += amountofSupply;//增加合约持有者的积分
    }
=======
This function ensures that the user's environment is capable of running the following code. It checks the existence of openssl ([-z String] would be true while the length of String is zero, so the first judgment means that the shell would stop running when there is no any version of openssl) and save the typre of current system into parameter OS.
+++
### Part Two - parse_params()

This part of code processes the options we set when implementing the shell file. Detailed explanation can refer to [the documents of FISCO BCOS][1]. For the previous Exercise on the first class, we used the -l option to specify the chain to be generated and the number of nodes under each IP.

[1]:https://fisco-bcos-documentation.readthedocs.io/zh_CN/latest/docs/manual/build_chain.html#id4 "the documents of FISCO BCOS"
+++
### Part Three - main()
#### 1. Option Check
First of all, we go to line 904.
>>>>>>> a06309d6a5943cb12da540b7bf86ffbd6e85be4e

 function getContractOwner() view public returns(address){
        return contract_holder;//增加一个查看合约持有者地址的函数
    }
```
+++
以下是对构造函数的修改
```solidity
constructor (uint256 initialSupply, string creditName,string creditSymbol) public{
        totalSupply =initialSupply;
        balances[msg.sender]=totalSupply;
        name=creditName;
        symbol=creditSymbol;
        contract_holder=msg.sender;//构造函数中添加合约持有者地址的初始化
    }
```
+++
2. 允许商家进行积分发放活动</br>
**构思：积分优惠活动指的是商家可以在活动期间为前来消费的消费者发送更多的积分，优惠的设置只能被合约持有者操控**</br>
+++
**具体实现：**</br>
以下是新增加的代码
```solidity
uint256 sale = 1;//储存优惠倍数，默认为1

function setSale(uint256 new_sale) public onlyOwner(msg.sender){
        sale=new_sale;//设置新的优惠倍数，只能由合约持有者操控
    }
    
    function getSale() view public returns(uint256) {
        return sale;//允许任何人查看当前优惠
    }
```
+++
以下是对_transfer函数的修改
```solidity
function _transfer(address _from,address _to,uint _value) internal{
        
        require(!(_to == 0x0),"The address shouldn't be the burning address!");
        require(balances[_from]>=_value,"No enough supply.");
        require(balances[_to]+_value > balances[_to],"Expected a positive value of supply.");
        
        uint previousBalances = balances[_from]+ balances[_to];
        if(msg.sender==contract_holder)//增加判断
        _value=_value*sale;//当传出积分者为合约持有者的时候应用优惠政策
        
        balances[_from] -= _value;
        balances[_to] += _value;
        
        emit transferEvent(_from,_to,_value);
        assert(balances[_from]+balances[_to] == previousBalances);
        
    }
```
<<<<<<< HEAD
=======
The code in line 920 and 921 call the **dir\_must\_not\_exists** function to checked that there is no such a file directory as nodes (the default value of **output_dir** is "nodes") and create the directory, else it'll throw an exception.
+++
#### 2. Binary File Processing
The code from line 929 to 959 checks whether we are using docker mode (if we use MacOs, we have to either use docker mode or use -e option to specific the path of fisco-bcos binary) . After that, it would download the the corresponding version of binary files or check the existing files to ensure the match of version.
+++
#### 3. Generate Certification Configuration 
In line 960 to 965, the bash uses **generate\_cert_conf** function to generate a certification configuration file or copy the designated file to the current directory.
+++
#### 4. CA key 
The code from line 976 to 991 would check whether we have an existing CA file. If not, the code would call the **gen_chain_cert** and **gen_agency_cert** function to generate ca.key.
+++
#### 5. GuoMi Chain(optional) CA key
The bash provides with a guomi_mode option that would enable the building of a blockchain of GuoMi version. If the option is set to true, the bash would call the **check_and_install_tassl** to first create a TASSL environment, and use **generate_cert_conf_gm** function to generate gmcert.cnf configuration file. The following process is similar to the described process in 4, while the functions are replaced by the GuoMi version, for instance, **gen_chain_cert** is replaced by **gen_chain_cert_gm**.
+++
#### 6. Generating Key 
The code from line 1008 to 1025 would set up the parameters that is related to the node generating for each IP server designated, and there is a double loop in the loop for every IP. 

Line 1026 to 1107 is a Double Loop. The outer level of Loop is determined by the numbers of nodes, it would first check the existence of the directory and throws exception when the directory already exists. 

The inner Loop would do the following:
+++
1. calls **gen_node_cert** to generate certification of nodes, create a configuration file directory(the default value of **conf_path** is conf), then removes the unwanted files and finally moves all the file in the current directory to the conf directory.
2. checks the length and the first two number of privateKey to ensure its legality, otherwise the whole node directory would be deleted.
3. does the similar privateKey checking when the GuoMi option is enabled. The differences are that conf_path is replaced by gm_conf_path and the privateKey of GuoMi should start with "00".

We now come back to the outer loop, this part of code does different operation to the configuration files in accordance with GuoMi or non-GuoMi, set the node_groups if we used -f option and set the nodeid_list if we used -l option.
+++
### Part Four - print_result()
![](https://github.com/marknash666/FiscoBcos-ExerciseOne/blob/master/image-ExerciseOne/print_result.png?raw=true)
This part of code is responsible for printing the execution results using **LOG_INFO** function, there is optional information according to the use of docker and IP list file.











>>>>>>> a06309d6a5943cb12da540b7bf86ffbd6e85be4e
