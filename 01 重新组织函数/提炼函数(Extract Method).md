## 提炼函数

### 1.场景（代码的坏味道）
+ 重复的代码
+ 过长的函数（函数复用率差）
+ 难以理解的代码（代码可读性差，可以放进独立的函数，赋予清晰的命名）

### 2. 关键点
#### 新函数命名（清晰的命名，表述函数的用途）
注意：提炼代码的时候，如果能够使用更好的名称来提炼代码，就应该毫不犹豫的提炼。如果找不到更合适的名称，就别动。
#### 语义距离
函数长度选择的关键在于函数名称与函数本地之间的语义距离，如果提炼能够强化代码清晰度，就撒手去做(即使函数名称长、代码短)

### 3. 快捷键
+ Mac(option+comand+M)


### 4. 案例
#### 1. 无局部变量

原始代码
```java
public void testA(){
    System.out.println("have a test");
}

public void testB(){
    System.out.println("have a test");
}
```

重构后代码
```java
public void testA(){
    printTest();
}

public void testB(){
    printTest();
}    

private void printTest() {
    System.out.println("have a test");
}
```
#### 2. 有局部变量

提炼的代码块具有局部变量，但是这些局部变量只是传值，并没有对局部变量进行修改

原始代码
```java
public void testA(){
    String name = "Mike";
    System.out.println("name:"+name);
}
```
重构代码
```java
public void testA(){
    String name = "Mike";
    printTest(name);
}

private void printTest(String name) {
    System.out.println("name:"+name);
}
```
#### 3. 对局部变量再赋值

原始代码
```java
void doOperate(){
    int total = 0;
    List<Integer> countList = new ArrayList();

    for(int count:countList){
        count += i;
    }

    System.out.println("get total count:"+total); 
}
```
重构代码
```java
void doOperate(){
    int total = 0;
    
    total = getTotalCount();
    System.out.println("get total count:"+total); 
}

int getTotalCount(){
    List<Integer> countList = new ArrayList();

    for(int count:countList){
        count += i;
    }

    System.out.println("get total count:"+total);
}
```





