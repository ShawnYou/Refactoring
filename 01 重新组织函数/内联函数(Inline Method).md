## 内联函数（Inline Method）

### 1.场景（代码的坏味道）
+ 函数本体与函数名称同样清晰(多余)

### 2.案例

原始代码
```java
int getRating(){
    return (moreThanFiveLateDeliveries())?2:1;
}

boolean moreThanFiveLateDeliveries(){
    return _numberOfLateDeliveries > 5;
}
```

重构后代码

```java
int getRating(){
    return (_numberOfLateDeliveries > 5) ? 2:1;
}
```
