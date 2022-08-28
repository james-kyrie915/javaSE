<h1 align="center"><b>Object Oriented Programming</b></h1>




[TOC]

# 面向对象中 

#### 继承性

```java
一、继承性的好处:
① 减少了代码的冗余，提高了代码的复用性
② 便于功能的扩展
③ 为之后多态性的使用，提供了前提

二、继承性的格式：Class A extends B{}
	A:子类、派生类、subclass
	B:父类、超类、基类、superclass
	
	2.1 体现：一旦子类A继承父类B以后，子类A中就获取了父类B中声明的所有的属性和方法
        特别的，父类中声明为private的属性或方法，子类继承父类以后，任然认为获取了父类中私有的结构。只是	
        因为封装性的影响，使得子类不能直接调用父类的结构而已。
    2.2 子类继承父类以后，还可以声明自己特有的属性或方法：实现功能的扩展。
        子类和父类的关系，不同于子集和集合的关系。
        extends：延展、扩展
        
三、Java中关于继承性的规定:
	1.一个类可以被多个子类继承。
	2.Java中类的单继承性:一个类只能有一个父类
	3.子父类是相对的概念。
	4.子类直接继承的父类，称为:直接父类。间接继承的父类，称为:间接父类
	5.子类继承父类以后，就获取了直接父类以及所有间接父类中声明的属性和方法
        
四、java.lang.Object类(根父类)的理解
	1．如果我们没有显式的声明一个类的父类的话，则此类继承于java.lang.Object类
	2．所有的java类（除java.lang.Object类之外）都直接或间接的继承于java.lang.Object类
	3．意味着，所有的java类具有java.lang.Object类声明的功能。
```

```java
1.为什么要有类的继承性? (继承性的好处)
*减少了代码的冗余，提高了代码的复用性
*便于功能的扩展
*为之后多态性的使用，提供了前提
```

图示：

![image-20220818004927760](../features/image-20220818004927760.png)

#### 方法的重写

```markdwon
方法的重写(override / overwrite)

1.重写:子类继承父类以后，可以对父类中同名同参数的方法，进行覆盖操作
2.应用:重写以后，当创建子类对象以后，通过子类对象调用子父类中的同名同参数的方法时，实际执行的是子类重写父类的方法
3.重写的规定：
    方法的声明：权限修饰符 返回值类型 方法名(形参列表) throws 异常的类型{
    	//方法体
	}
	约定俗成：子类中的叫重写的方法，父类中的叫被重写的方法
  ① 子类重写的方法的方法名和形参列表与父类被重写的方法的方法名和形参列表相同
  ② 子类重写的方法的权限修饰符不小于父类被重写的方法的权限修饰符
		>特殊情况:子类不能重写父类中声明为private权限的方法
  ③ 返回值类型：
		>父类被重写的方法的返回值类型是void，则子类重写的方法的返回值类型只能是void
		>父类被重写的方法的返回值类型是A类型，则子类重写的方法的返回值类型可以是A类或A类的子类
		>父类被重写的方法的返回值类型是基本数据类型(比如：double)，则子类重写的方法的返回值类型必须是相同的基本数据类型(必须也是double)
  ④ 子类重写的方法抛出的异常类型不大于父类被重写的方法抛出的异常类型
****************************************************************************************
  子类和父类中的同名同参数的方法要么都声明为非static的(考虑重写)，要么都声明为static的(不是重写)
```


#### super关键字

```java
1.super理解为：父类的
2.super可以用来调用：属性、方法、构造器
    
3.super的使用：
    3.1 我们可以在子类的方法或构造器中。通过使用"super.属性"或"super.方法"的方法，显式的调用父类中声明的属性或方法。但是，通常情况下，我们习惯省略"super."
    3.2 特殊情况：当子类和父类中定义了同名的属性时，我们要想在子类中调用父类中声明的属性，则必须显式的使用"super.属性"的方式，表明调用的是父类声明的属性。
    3.3 特殊情况：当子类重写了父类中的方法以后，我们想在子类的方法中调用父类中被重写的方法时，则必须显式的使用"super.方法"的方式，表明调用的是父类中被重写的方法。
    
4.super调用构造器
    4.1 我们可以在子类的构造器中显式的使用"super(形参列表)"的方式，调用父类中声明的指定的构造器
    4.2 "super(形参列表)"的使用，必须声明在子类构造器的首行
    4.3 我们在类的构造器中，针对于"this(形参列表)"或"super(形参列表)"只能二选一，不能同时出现
    4.4 在构造器的首行，没有显式的声明"this(形参列表)"或"super(形参列表)"，则默认调用的是父类中空参的构造器：super();
	4.5 在类的多个构造器中，至少有一个类的构造器中使用了"super(参数列表)"，调用父类中的构造器
```

#### 子类对象实例化的全过程

```java
1. 从结果上来看：(继承性)
    子类继承父类以后，就获取了父类中声明的属性或方法。
    创建子类的对象，在堆空间空，就会加载所有父类中声明的属性
    
2. 从过程上来看：
    当我们通过字类的构造器创建子类对象是，我们一定会直接或间接的调用父类的构造器，进而调用父类的父类的构造器,...知道调用了java.lang.Object类中空参的构造器为止。正因为加载过所有的父类的结构，所以才可以看到内存中有父类中的结构，子类对象才可以考虑进行调用。 
    
明确：虽然创建子类对象时，调用了父类的构造器，但是自始至终就创建过一个对象，即为new的子类对象。
```

![image-20220820235621956](../features/image-20220820235621956.png)

思考：

1. super(...)和this(...)只能在构造器的首行出现

2. 无论通过哪个构造器创建子类对象，需要保证先初始化父类。
   目的:当子类继承父类后，“继承“父类中所有的属性和方法，因此子类有必要知道父类如何为对象进行初始化

![image-20220820132408989](../features/image-20220820132408989.png)

![image-20220820131831774](../features/image-20220820131831774.png)

#### 多态性

```java
1.理解多态性：可以理解为一个事物的多种形态。
2.何为多态性：
	对象的多态性：父类的引用指向子类的对象（或子类的对象赋给父类的引用）
3.多态的使用：虚拟方法调用
    有了对象的多态性以后，我们在编译期，只能调用父类中声明的方法，但在运行期，我们实际执行的是子类重写父类的方法。
    总结：编译看左边，运行看右边。
4.多态性的使用前提：① 类的继承关系 ② 方法的重写 
5.对象的多态性，只适用于方法，不适用于属性（编译和运行都看左边）
```

```java
//多态性的使用举例一:
public class AnimalTest {
    public static void main(String[] args) {
		AnimalTest test = new AnimalTest();
        test.func(new Dog());
	}
    
    //多态的调用
    public void func(Animal animal){//Animal animal = new Dog();
		animal.eat();
		animal.shout();
    }
    
    //没有多态性的调用
//    public void func(Dog dog){
//        dog.eat();
//        dog.shout();
//    }
//    public void func (cat cat)i
//        cat.eat();
//        cat.shout( );
//    }
}

class Animal{
    public void eat(){
    	System.out.print1n("动物:进食");
    }
    
    public void shout(){
	    system.out.println("动物:叫");
    }
}

class Dog extends Animal{
	public void eat(){
    	System.out.print1n("狗吃骨头");
    }
    
    public void shout(){
	    system.out.println("汪！汪！汪");
    }
}

class Cat extends Animal{
	public void eat(){
    	System.out.print1n("猫吃鱼");
    }
    
    public void shout(){
	    system.out.println("喵！喵！喵");
    }
}
```

```java
//举例二:
class Order{
    public void method (object obj){
        
    }
}
```

```java
//举例三:
class Driver{
    
    public void doData(Connection conn){//conn = new MySQLConnection();
    									//coon = new OracleConnection(); 
		//规范的步骤去操作数据
        coon.method3();
        coon.method3();
        coon.method3();

    }
}
```

#### 方法的重载和重写区别

```java
1.二者的定义细节:略

2、从编译和运行的角度看:
重载，是指允许存在多个同名方法，而这些方法的参数不同。编译器根据方法不同的参数表，对同名方法的名称做修饰。对于编译器而言，这些同名方法就成了不同的方法。它们的调用地址在编译期就绑定了。Java的重载是可以包括父类和子类的，即子类可以重载父类的同名不同参数的方法。
所以:对于重载而言，在方法调用之前，编译器就已经确定了所要调用的方法,这称为“早绑定”或“静态绑定”;

而对于多态，只有等到方法调用的那一刻，编译器才会确定所要调用的具体方法，这称为“晚绑定”或“动态绑定”。

引用一句Bruce Eckel的话:“不要犯傻，如果它不是晚绑定，它就不是多态。”
```

#### instanceof关键字

```java
向下转型：使用强制类型转换

使用情境:为了避免在向下转型时出现ClassCastException的异常，我们在向下转型之前，先进行instanceof的判断，一旦返回true，就进行向下转型。如果返回false，不进行向下转型。

如果a instanceof A返回true，其中，类B是类A的父类，则a instanceof B也返回true
```

#### java.lang.Object类

```java
1.Object类是所有Java类的根父类
2.如果在类的声明中未使用extends关键字指明其父类，则默认父类为java.lang.Object类
3.Object类中的功能（属性、方法）具有通用性
    属性：无
    方法：equals() / toString() / getClass() / hashCode() / clone() / finalize()
    	 wait() / notify() / notifyAll()
4.Object类只声明了一个空参的构造器

面试题：final、finally、finalize的区别？

```

#### equals()和==的区别

```java
一、回顾==的使用：
== ：运算符
1.可以使用在基本数据类型变量和引用数据类型变量中
2.如果比较的是基本数据类型变量：比较两个变量保存的数据是否相等。（不一定类型要相同）
  如果比较的是基本数据类型变量：比较两个对象的地址值是否相同，即两个引用是否指向同一个对象。
补充：== 符号使用时，必须保证符号左右两边的变量类型一致。

二、equals()方法的使用：
1.是一个方法，而非运算符
2.只能使用于引用数据类型
3.Object类中equals()的定义：
    public boolean equals(Object obj){
    	return (this == obj);
	}
	说明：Object类中定义的equals()和==的作用是相同的：比较两个对象的地址值是否相同，即两个引用是否指向同一个对象。
4.像String、Date、File、包装类等都重写了Object类中的equals()方法，比较的不是两个引用的地址是否相同，而是比较两个对象的"实体内容"是否相同。
5.通常情况下，我们自定义的类如果使用equals()的话，也通常是比较两个对象的"实体内容"是否相同。那么我们就需要对Object类的equals()进行重写
  重写的规则：比较两个对象的实体内容

```

![image-20220821133629568](../features/image-20220821133629568.png)

#### toString()方法

```java
Object类型中toString()的使用：
1.当我们输出一个对象的引用时，实际上就是调用当前对象的toString()方法
2.Object类中toString()的定义：
    public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }

3.像String、Date、FIle、包装类等都重写了Object类中的toString()方法
  使得在调用对象的toString()时，返回"实体内容"信息
4.自定义类也可以重写toString()方法，当调用此方法时，返回对象的"实体内容"
```

#### 单元测试

```java
Java中的Junit单元测试

步骤：
1.创建Java类，进行单元测试
    此时的Java类要求：① 此类是public的 ② 此类提供公共的无参的构造器
2.此类中声明单元测试方法
    此时的单元测试：方法的权限是public，没有返回值，没有形参
3.此单元测试方法上需要声明注解：@Test，并在单元测试类中导入：import org.junit.Test;
（idea中,停留在@Test行，ALT + enter键导入）
4.声明好单元测试方法以后，就可以在方法体内测试相关的代码
5.写完代码以后，在方法体代码中，点击鼠标左键，选择运行方法体的代码

说明：
    1.如果执行结果没有任何异常：绿条
    2.如果执行结果出现异常：红条
```

#### 包装类(Wrapper)

```java
1.java提供了8种基本数据类型对应的包装类，使得基本数据类型的变量具有类的特征
2.掌握的：基本数据类型、包装类、String三者之间的相互转换


```

```java
//基本数据类型--->包装类：调用包装类的构造器
//包装类--->基本数据类型：调用包装类的xxxxValue()
实例：
    Integer integer = new Integer(100);
    int i = integer.intValue();

-------------------------------------------------
基本数据类型、包装类--->String类型：调用String重载的valueOf(Xxx xxx)
//方式一：连接运算
    int num1 = 10;
    String str1 = num1 + "";
//方式2：调用String的valueOf(Xxx xxx)
    float f1 = 12.3f;
    String str2 = String.valueOf(f1);//"12.3"
    Double dou1 = new Double(12.4);
    String str3 = String.valueOf(dou1);"12.4"

String类型--->基本数据类型、包装类：调用包装类的parseXxx()
    String str1 = "123";
    int num1 = Integer.parseInt(str1);
    String str2 = "true";
    boolean bl1 = Boolean.parseBoolean(str2);
```

##### 自动装箱与拆箱

```java
JDK 5.0新特性：自动装箱与拆箱
//自动装箱：基本数据类型--->包装类
    int num1 = 10；
    Integer integer1 = num1;//自动装箱

	boolean b1 = true;
	Boolean boolean1 = b1;//自动装箱

//自动拆箱：包装类--->基本数据类型
	int num2 = integer1;
	boolean b2 = boolean1;
```

#### 包装类面试题

```java
关于包装类使用的面试题

题1：
    Object o1 = true ? new Integer(1) : new Double(2.0);
    System.out.println(o1);//1.0
    三元运算符中需要统一数据类型

    Object o2 ;
    if (true)
        o2 = new Integer(1);
    else
        o2 = new Double(2.0);
    System.out.println();//1
---------------------------------------------
题2：
	Integer i = new Integer(1);
	Integer j = new Integer(1);
    System.out.println(i == j);//false

    //Integer内部定义了IntegerCache类，工ntegerCache类中定义了Integer[],
    //保存了从-128~127范围的整数。如果我们使用自动装箱的方式，给Integer赋值的范围在
    //-128~127范围内时，可以直接使用数组中的元素，不用再去new了。目的:提高效率

    Integer m = 1;
    Integer n = 1;
    System.out.println(m == n);//true
    Integer x = 128;//相当升new了一个Integer对象
    Integer y = 128;//相当升new了一个Integer对象
    system.out.println(x == y);//false
```

#### 复习回顾

```java
1.关于向上转型和向下转型：
    1.1 向上转型：多态
    1.2 向下转型：
    	1.2.1 为什么使用向下转型：
    		有了对象的多态性以后，内存中实际上是加载了子类特有的属性和方法的，但是由于变量声明为父类类
    		型，导致编译时，只能调用父类中声明的属性和方法。子类特有的属性和方法不能调用。如何才能调用
    		子类特有的属性和方法？使用向下转型

    	1.2.2 如何实现向下转型：
    		使用强制类型转换符
    	
    	1.2.3 使用时的注意点：
    		① 使用强转时，可能出现ClassCastException的异常
    		② 为了避免在向下转型时出现ClassCastException的异常，我们在向下转型之前，先进行
    		  instanceof的判断，一旦返回true，就进行向下转型。如果返回false，不进行向下转型

		1.2.4 instanceof的使用
    		① a instanceof A：判断对象a是否是类A的实例。如果是，返回true；如果不是返回false
			② 如果a instanceof A返回true，其中，类B是类A的父类，则a instanceof B也返回true
    		③ 要求a所属的类与类A必须是子类和父类的关系，否则编译错误
    	
    	1.2.5 图示：如下图（../features/image-20220822235330578.png）


面试题：
    1.谈谈你对多态性的理解？
    	① 实现代码的通用性
		② 举例: Object类中定义的public boolean equals(Object obj){}
			   JDBC：使用java程序操作(获取数据库连接、CRUD)数据库(MySQL、Oracle、SQL Server)
		③ 抽象类、接口的使用肯定体现了多态性。（抽象类、接口不能实例化）
	
	2.多态是编译时行为还是运行时行为？
		运行时行为
import java.util.Random;

class Animal{

    protected void eat(){
        System.out.println("animal eat food");
    }
}

class Dog extends Animal{

    public void eat(){
        System.out.println("dog eat bone");
    }
}

class Cat extends Animal{

    public void eat(){
        System.out.println("cat eat fish");
    }
}

class Sheep extends Animal{

    public void eat(){
        System.out.println("sheep eat grass");
    }
}
	
public class AnimalTest{
    
    public static void main(String[] args){
        int key = new Random().nextInt(3);
        
        Animal animal = new AnimalTest().getInstance(key);
        animal.eat();
    }
    
    public Animal getInstance(int key){
		switch(key){
            case 0:
                return new Dog();
            case 1:
                return new Cat();
            default:
                return new Sheep();
        }
    }
}
```

![image-20220822235330578](../features/image-20220822235330578.png)
