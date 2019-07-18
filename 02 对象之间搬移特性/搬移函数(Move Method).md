## 搬移函数

### 1. 场景（代码的坏味道）
+ 一个类有太多行为，这些行为依赖的类比较多，与其他类形成高度耦合。

### 2. 案例
原始代码   
```java
Class Account{
    //账户类型
    private AccountType _type;
    private int _dayOverDraw;

    //透支金额计算规则
    double overdraftCharge(){
        if(_type.isPremiun()){
            double result = 10;
            if(_dayOverDraw > 7){
                result += (_dayOverDraw - 7)*0.85;
            }
        }else{
            return _dayOverDraw*1.75;
        }
    }

    double bankCharge(){
        double result = 4.5;
        if(_dayOverDraw >0){
            result += overdraftCharge();
        }
        return result;
    }
}
```   
#### 代码分析
1. 观察哪些函数行为与其他类有过多联系。
overdraftCharge()为透支金额计算规则，与AccountType有行为依赖，且不同的账户具有不同的计算规则，应该把overdraftCharge()方法搬移到AccountType类中
2. 观察被搬移函数的每一项特性，看是否需要跟随函数一起搬移。
overdraftCharge()引用了变量_dayOverDraw，_dayOverDraw随着不同账户而不同，所以应该保留在Account中。

特性搬移的四种选择
+ 直接将特性搬移到目标类(将_dayOverDraw搬移到AccoutType)
+ 建立或者使用从目标类到源类的引用关系
+ 将源对象以参数的形式传递给目标类
+ 所需特性为变量，则作为参数传递给目标函数。（采用）

重构后代码
```java
Class Account{
    private AccountType _type;

    double bankCharge(){
        double result = 4.5;
        if(_dayOverDraw > 0){
            result += _type.overdradtCharge(_dayOverdraw);
        }
        return result;
    }
}

Class AccountType{
    double overdraftCharge(int daysOverdraw){
        if(isPremium()){
            double result = 10;
            if(dayOverDraw > 7){
                result += (daysOverDraw - 7)*0.85;
            }
            return result;
        }
        return dayOverdraw * 1.75;
    }
}

```

> 如果需要源类的多个特性，可以将源对象传递给目标函数，但是如果目标函数需要太多的特性，则设计不合理，需要进一步重构，分解目标函数。



