## 分解临时变量

### 1. 场景（代码的坏味道）
+ 临时变量（排除循环变量和计算结果）被赋值多次，承担了多个责任

### 2. 案例

原始代码
```java
double temp = 2* (_height + _width);
temp = _height * _width;
```

重构代码
```java
final double perimeter = 2* (_height + _width);
final double area = _height * _width; 
```