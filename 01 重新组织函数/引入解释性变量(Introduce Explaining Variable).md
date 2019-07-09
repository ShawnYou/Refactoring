## 引入解释性变量

### 1. 场景（代码的坏味道）
+ 表达式很复杂，难以看清其表达意图、难以阅读

### 2. 关键点
+ 可以使用(Extract Method)来替代(Introduce Explaining Variable),当(Extract Method)难以进行的时候才使用(Introduce Explaining Variable)
+ 

### 3. 案例

原始代码
```java
if ((platform.toUpperCase().indexOf("mac") > -1) &&
    (brower.toUpperCase().indexOf("ie") > -1) &&
    wasInitializes() && resize > 0) {
        ......
    }
```

重构代码(Introduce Explaining Variable)

```java
final boolean isMacOS = platform.toUpperCase().indexOf("mac") > -1;
final boolean isIEBrowser = brower.toUpperCase().indexOf("ie") > -1;
final boolean wasResized = resize > 0;

if (isMacOS && isIEBrowser && wasInitializes() && wasResized) {
    ......
}
```

重构代码(Extract Method)
```java
private boolean isMacOs(){
    return platform.toUpperCase().indexOf("mac") > -1;
}

private boolean isIEBrowser(){
    return brower.toUpperCase().indexOf("ie") > -1;
}

private boolean wasResized(){
   resize > 0; 
}

if (isMacOS && isIEBrowser && wasInitializes() && wasResized) {
    ......
}
```