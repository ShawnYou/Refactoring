## 移除对参数的赋值

### 1. 场景（代码的坏味道）
+ 对参数进行赋值

### 2. 关键点
+ 对象作为传参传入某个函数，对参数赋值会导致传参对象的改变，使其引用了另一个对象。

### 3. 案例

```java
int discount (int inputVal, int quantity, int yearToDate) {
    if (inputVal > 50) inputVal -= 2;
}
```

```java
int discount (int inputVal, int quantity, int yearToDate) {
    int result = inputVal;
    if (result > 50) result -= 2;
}
```