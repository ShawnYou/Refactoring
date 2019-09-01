## 引入外加函数

### 代码的坏味道
为提供服务的类增加一个函数，但是你无法修改这个类。

### 分析
在客户类中建立一个函数，并以第一参数的形式传入一个服务类实例

### 实例代码

#### 原始代码
```java
Date newStart = new Date(previousEnd.getYear(),previousEnd.getMonth(),previousEnd.getDay()+1)
```

#### 重构代码
增加一个外部函数来包装服务类提供的方法
```java
Date newStart = nextDay(previousEnd);

private static Date nextDay(Date arg){
    return new Date(arg.getYear(),arg.getMonth(),arg.getDate()+1);
}
```

### 小结
+ 外加函数的方式实现的这一项功能，本应该在服务类实现的。
+ 一个服务类创建了大量的外加函数或者很多类都需要这样的外加函数，这时候不应该使用此项重构方法，应该使用(引入本地扩展)