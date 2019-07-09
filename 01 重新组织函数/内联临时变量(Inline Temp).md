## 内联临时变量

### 1. 场景（代码的坏味道）
+ 一个临时变量，只被简单的表达式赋值过一次

### 2. 案例

原始代码
```java
double basePrice = anOrder.basePrice();
return (basePrice > 1000);
```

重构后代码
```java
return （anOrder.basePrice()>1000）
```