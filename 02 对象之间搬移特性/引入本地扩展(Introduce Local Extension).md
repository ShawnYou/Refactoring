## 引入本地扩展

### 代码的坏味道
需要为服务类提供一些额外的函数，但是却无法修改这个服务类

### 分析
建立一个新类，使他包含这些额外函数，让这个扩展品成为源类的子类或者包装类
+ 子类化(使用继承)
```java
class MfDateSub extends Date{
    Date nextDay(){
        return new Date(getYear(),getMonth(),getDate()+1);
    }
}
```
扩展类具有获取第二天日期的功能。

+ 包装

```java
class MfDateWrap{
    private Date original;

    public MfDateWrpa(String dateString){
        original = new Date(dateString);
    }
}
```

