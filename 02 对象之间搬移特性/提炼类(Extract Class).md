## 提炼类

### 1.场景(代码的坏味道)
一个类做了两个类的事情

### 2. 案例

原始代码
```java
@Data
class Person{
    private String name;
    private String officeAreaCode;
    private String officeNumber;
}
```
1. Person类既包含Person的信息，又包含电话号码的信息，由此将电话号码的信息分离到一个单独的类。

重构后代码
```java
class Person{
    private TelePhoneNumber phoneNumber = new TelePhoneNumber(); 
}
```

### 注意点
+ 新类的访问权限

                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               