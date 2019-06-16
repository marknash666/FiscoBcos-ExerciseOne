# LAGCredit合约阅读分析

## 代码分析
1. 数据、事件定义
```
string name = "LAGC";//默认积分名称
string symbol = "LAG";//默认积分代号
uint256 totalSupply;//积分总量
mapping (address => uint256) private balances;//记录账号持有积分数目的结构体(key为address，value为uint256)
event transferEvent(address from, address to,uint256 value);//定义了一个名为transferEvent的事件，该事件会被Web3.js监听并作出响应
```

2. 构造函数
```
constructor (uint256 initialSupply, string creditName,string creditSymbol) public{
        totalSupply =initialSupply;//初始化积分总量
        balances[msg.sender]=totalSupply;//初始化合约持有者的积分数
        name=creditName;//初始化积分名称
        symbol=creditSymbol;//初始化积分代号        
    }
```

3. getTotalSupply
```
function getTotalSupply() view public returns (uint256){
        return totalSupply;//用于查看当前积分总量的函数
    }
```

4. _transfer(internal的传递执行体)
```
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

5. transfer(封装了内部执行的积分传递函数)
```
function transfer(address _to, uint256 _value) public {
        _transfer(msg.sender,_to,_value);//将调用者的地址并与其余两个参数传给实际执行体
    }
```

6.balanceOf
 function balanceOf(address _owner) view public returns(uint256){
        return balances[_owner];//查看传入地址所拥有的积分数
    }