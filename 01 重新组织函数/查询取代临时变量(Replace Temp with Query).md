## 查询取代临时变量

### 1. 场景（代码的坏味道）
+ 临时变量保存某一表达式运算结构
+ 临时变量太多，不利于维护
+ 局部变量会使(Extract Method)难以提炼

### 2. 好处
使用查询式代替临时变量

+ 代码更加清晰、整洁
+ 利于提炼函数

### 3. 案例

```java
int area = _length * _width;
if (area > 1000) 
    return area * 5;
else
    return area *4;
```

```java
if (area() > 1000) 
    return area() * 5;
else
    return area() *4;
    
int area() {
    return _length * _width;
}
```