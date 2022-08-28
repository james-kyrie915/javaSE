<h1 align="center"><b>Object Oriented Programming</b></h1>




[TOC]

# 面向对象下

#### static关键字

```markdown
1.static：静态的
2.static可以用来修饰：属性、方法、代码块、内部类

3.使用static修饰属性：静态变量（或类变量）
    3.1 属性，按是否使用static修饰，又分为：静态属性 VS 非静态属性(实例属性)
      实例变量：我们创建类的多个对象，每个对象都独立的拥有一套类中的非静态属性。当修改其中一个对象中的非静态属性时，不会导致其它对象中同样的属性值得修改。
      静态变量：我们创建了类的多个对象，多个对象共享同一个静态变量。当通过某一个对象修改静态变量时，会导致其他对象调用此静态变量时，是修改过了的。
    3.2 static修饰属性的其他说明：
    	① 静态变量随着类的加载而加载。可以通过"类.静态变量"的方式进行调用
    	② 静态变量的加载要早于对象的创建。
    	③ 由于类只会加载一次，则静态变量在内存中也只会存在一份：存在方法区的静态域中。
    	
    	调用
		④ 		类变量		实例变量
    	类	    yes			no
    	对象	   yes		   yes
	3.3 静态属性举例：System.out; Math.PI;

4.使用static修饰方法：静态方法
	① 随着类的加载而加载，可以通过"类.静态方法"的方式进行调用
    
    调用
	② 		静态方法	非静态方法
    类	    yes			no
    对象	   yes		   yes
	③ 静态方法中，只能调用静态的方法或属性
	  非静态方法中，既可以调用非静态的方法或属性，也可以调用静态的方法或属性

5.static注意点：
	5.1 在静态的方法内，不能使用this关键字、super关键字
	5.2 关于静态方法和静态属性的使用，从生命周期的角度去理解

6.开发中，如何确定一个属性是否要声明为static的？
		> 属性是可以被多个对象所共享的，不会随着对象的不同而不同的
		> 类中的常量也常常声明为static
		
  开发中，如何确定一个方法是否要声明为static的？
  		> 操作静态属性的方法，通常设置为static的
  		> 工具类中的方法，习惯上声明为static的。比如：Math、Arrays、Collections
```

#### 单例设计模式 

```java
单例设计模式:
1．所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能存在一个对象实例。

2．如何实现?
	饿汉式 VS 懒汉式
    
3.区分饿汉式和懒汉式
    饿汉式:
        坏处:对象加载时间过长。
        好处:饿汉式是线程安全的
	懒汉式:
		好处:延迟对象的创建。
		目前的写法坏处:线程不安全。--->到多线程内容时，再修改
```

```java
//饿汉式
public class singletonTest1{
    public static void main(String[] args) {
        Bank bank1 = Bank.getInstance();
    	Bank bank2 = Bank.getInstance();
		System.out.println(bank1 == bank2);
    }
}

class Bank{
    //1.私有化类的构造器
    private Bank(){
	
    }
    
    //2.内部创建类的对象
    //4.要求此对象也必须声明为静态的
    private static Bank instance = new Bank();
    
    //3.提供公共的方法，返回类的对象
    public static Bank getInstance(){
    	return instance;
    }
}
```

```java
//懒汉式
public class singletonTest2 {
    
}

class Order{
    //1.私有化类的构造器
    private Order(){
        
    }
    
    //2.声明当前类对象，没有初始化//4.此对象也必须声明为static的
    //4.要求此对象也必须声明为静态的
    private static Order instance = null;
    
    //3.声明public、 static的返回当前类对象的方法
    public static Order getInstance(){
        if(instance == null){
            instance = new Order();
        }
    	return instance;
    }
}
```

#### main方法

```java
main()方法的使用说明:
1. main()方法作为程序的入口
2. main(()方法也是一个普通的静态方法
3. main()方法可以作为我们与控制台交互的方式。(之前:使用Scanner)
```

```java
public class MainTest{
    public static void main(String[] args) {//入口
        
        Main.main(new string[100]);
        
        MainTest test = new MainTest();
        test.show();
    }
    
    public void show(){
        
    }
}

class Main{
    public static void main(String[] args) {
        for(int i = e;i < args.length;i++){
            args[i] = "args_" + i;
            System.out.println(args[i]);
        }
    }
}
```

#### 代码块

```java
类的成员之四：代码块(或初始化块)

代码块执行：由父及子，静态先行

1．代码块的作用:用来初始化类、对象
2．代码块如果有修饰的话，只能使用static.
3．分类：静态代码块 vs 非静态代码块

4．静态代码块
	> 内部可以有输出语句
    > 随着类的加载而执行，而且只执行一次
    > 初始化类的信息
    > 如果一个类中定义了多个静态代码块，则按照声明的先后顺序执行
    > 静态代码块的执行要优先于非静态代码块的执行
    > 静态代码块内只能调用静态的属性、静态的方法，不能调用非静态的结构

5. 非静态代码块
	> 内部可以有输出语句
	> 随着对象的创建而执行
    > 每创建一个对象，就执行一次非静态代码块
    > 作用：可以在创建对象时，对对象的属性等进行初始化
	> 非静态代码块内可以调用静态的属性、静态的方法，或非静态的属性、非静态的方法
    
对属性可以赋值的位置:
①默认初始化
②显式初始化/⑤在代码块中赋值
③构造器中初始化
④有了对象以后，可以通过"对象.属性"或"对象.方法"的方式，进行赋值
执行先后顺序：① - ②/⑤ - ③ - ④
```

#### final关键字

```java
final:最终的

1. final可以用来修饰的结构：类、方法、变量

2. final用来修饰一个类：此类不能被其他类继承。
	比如：String类、System类、StringBuffer类

3. final用来修饰方法：表明此方法不可以被重写
	比如：Object类中getClass();

4. final用来修饰变量：此时的"变量"就称为一个常量
	4.1 final修饰属性：可以考虑赋值的位置有：显式初始化、代码块中初始化、构造器中
	4.2 final修饰局部变量:
		尤其是使用final修饰形参时，表明此形参是一个常量。当我们调用此方法时，给常量形参赋一个实参。一旦赋
		值以后，就只能在方法体内使用此形参，但不能进行重新赋值。

static final 用来修饰属性：全局常量
```

#### native关键字

```java
native方法往下走可能就是调底层的C、C++代码，不对外开放
```

