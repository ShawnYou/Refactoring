## 自封装字段

### 代码的坏味道(场景)
直接访问一个字段的场景下，如果对这个字段的数据进行扩展，即想要更加灵活的数据管理方式就显得很麻烦。

重构前代码
```java
class IntRange{
    private int low;
    private int high;

    boolean includes(int arg){
        return arg >= low && arg <= high;
    }

    void grow(int refactor){
        high = high * refactor;
    }
}
```

> 如果想要访问超类的一个字段，想在子类中将这个字段变量的访问改成另外一个值，想要一种更加灵活的数据管理方式。我们就需要(自封装字段)这种重构方式。子类可以根据需要重写取值和设值函数。

重构后代码
```java
class IntRange{
    private int low;
    private int high;

    boolean includes(int arg){
        return arg >= low && arg <= high;
    }

    void grow(int refactor){
        getHigh()*refactor;
    }

    int getLow(){
        return low;
    }

    int getHigh(){
        return high;
    }

    void setHigh(){
        this.high = high;
    }

    void setLow(){
        this.low = low;
    }
}
```

```java
class CappeRange extends IntRange{

    private int cap;

    public CappeRange(int low,int high,int cap){
        super(low,high);
        cap = cap;
    }

    int getCap(){
        return cap;
    }

    int getHigh(){
        Math.min(super.getHigh(),getCap);
    }
}
```

+ 子类重写了getHigh()的逻辑，加入了新的判断，而没有修改IntRange类里面getHigh的逻辑。

