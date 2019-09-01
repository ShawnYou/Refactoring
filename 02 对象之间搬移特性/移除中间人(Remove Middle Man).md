## 移除中间人

### 代码的坏味道
某个类做了过多的简单委托动作，每当客户想要使用受托类的新特性，就必须在服务端添加一个简单委托函数，一旦受拖类的特性越来越多，类里面就有过多的简单委托函数，不好维护。

### 实例代码

将委托类暴露出来
#### 重构代码
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

### 小结
到底该是移除中间人 还是隐藏委托类，这个没有固定的尺度，随着系统运行过程中不断调整。
重构的意义在于----永远不要说对不起。
