## 搬移字段

### 1. 场景(代码的坏味道)
某个字段被所属类之外的其他类所频繁用到。

### 2. 案例

原始代码
```java
class Account{
    private AccountType _type;
    private double _interestRate;

    double interestForAmount_days(double amount, int days){
        return _interestRate * amount * days /365;
    }
}
```

#### 代码分析
+ _interestRate经常被AccountType类用到，所以考虑将_interestRate搬移到目标类(AccountType)

重构代码
```java
class AccountType{
    private double _interestRate;

    void setInterestRate(double arg){
        _interestRate = arg;
    }

    double getInterestRate(){
        return _interestRate;
    }
}

class Account{
    private AccountType _type;

    double interestForAmount_days(double amount, int days){
        return  _type.getInterestRate()* amount * days /365;
    }
}

```

