## 隐藏委托关系

### 1. 场景(代码的坏味道)

客户通过一个委托类来调用另一个对象(客户必须知道这一中委托关系，才能够正确的调用，万一委托关系发生变化，客户也得做相应的调整)

### 2. 案例

#### 1. 原始代码

```java
Class Person{
    Department department;

    public Department getDepartment(){
        return department;
    }
}

Class Department{
    private Person manageer;

    publlic Person getManager(){
        return mnanager;
    }
}
```
如果客户想要知道Aaron的经理是谁， 那么就必须通过aaron.getDepartment().getManager();

缺点：暴露了关系，客户可以知道Department与Manager之间的关系。 

方案：隐藏委托关系，不向客户暴露department信息。

#### 2. 重构代码

在Person类建立委托函数, 对客户隐藏的细节。
```java
public Person getManager(){
    return department.getManager();
}
```