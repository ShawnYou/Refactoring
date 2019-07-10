## 函数对象取代函数

### 1. 场景（代码的坏味道）
+ 大型函数，局部变量的使用导致无法使用Extract Method

### 2. 关键点
+ 将函数放进单独的对象中，由此局部变量就变成了对象内的字段，由此可以通过Extract Method进行提取，可以省去很多局部变量的麻烦

### 3. 案例

原始代码
```java
Class Account{
    int gamma(int inputVal,int quantity,int yearToDate){
        int importantValue1 = (inputVal * quantity) + delta();
        int importantValue2 = (inputValue * yearToDate) + 100;
        if(yearToDate - importantValue1) >100){
           importantValue2 -= 20; 
        }
        int importantValue3 = importantValue2 * 7;
        return importantValue3 - 2* importantValue1;
    }
}
```
```java
如果对这块代码进行Extract Method的话，局部变量不好处理
if(yearToDate - importantValue1) >100){
   importantValue2 -= 20; 
}
```

重构后代码
```java
Class Ganma{
    private final Account account;
    private int inputValue;
    private int quantity;
    private int yearToDate;
    private int importantValue1;
    private int importantValue2;
    private int importantValue3;

    //构造函数
    Gamma(Account account,int inputValue,int quantity,int yearToDate){
        account = account;
        inputValue = inputValue;
        quantity = quantity;
        yearToDate = yearToDate;
    }

    //以前函数的逻辑集中在compute()里面
    int compute(){
        int importantValue1 = (inputVal * quantity) + account.delta();
        int importantValue2 = (inputValue * yearToDate) + 100;
        if(yearToDate - importantValue1) >100){
           importantValue2 -= 20; 
        }
        int importantValue3 = importantValue2 * 7;
        return importantValue3 - 2* importantValue1; 
    }
}

Class Account{
    int ganma(int inputVal,int quantity,int yearToDate){
        return new Gamma(this,inputValue,quantity,yearToDate).compute();
    }
}

```

经过重构后，所有的局部变量都存在与函数对象中，由此我们可以尽情的Extract Method而不需考虑局部变量的影响。

```java
int compute(){
    int importantValue1 = (inputVal * quantity) + account.delta();
    int importantValue2 = (inputValue * yearToDate) + 100;
    //extract method
    importThing();
    int importantValue3 = importantValue2 * 7;
    return importantValue3 - 2* importantValue1; 
}

void importThing(){
   if(yearToDate - importantValue1) >100){
       importantValue2 -= 20; 
    } 
}



```


