---
title: Java反射机制
date: 2017-09-02 20:16:58
tags: [java,反射]
categories: java
---
反射机制  java.lang.reflect

jvm->ClassLoader->Class -> all Object 
->类使用{ 加载，链接，初始化{static 方法（构造器隐式），域} }
->初始化 static 块{ .class没有 ，Class.forName( "ClassName")有 }
->生成Class对象{1.Class.forName( "ClassName")、2..class、3. new Object().getClass }
-> 泛型<? super SubClass>表示SuperClass
 -> 类型转换{ Class.cast() 、instanceOf 、Class.isInstance }
->调用  Class Method等 （共有）  DeclaredMethod(本类声明的方法)
 setAccessible(true) 访问限制的
Method第二个参数     类型Class对象:int.class,String.class等
method.invoke()执行方法



一、jvm->类加载器(动态加载)->Class对象->生成所有对象

类使用准备工作->加载，链接，初始化

加载->查找字节码创建Class对象 

链接->验证字节码，为静态域创建分配内存空间 

初始化->
 执行超类静态初始化器和静态初始化块,执行本类的静态初始化器和静态初始化块 

初始化被延时到，static (非 static
final)域/方法(构造器，暗中也是静态的) 首次执行时才执行。

二、 Class：
泛型，编译时检查。<? super 子类> 是什么超类
1.Classs.forName() 有初始化
2.类字面常量（类名.class）boolean.class=Boolean.TYPE等 无初始化
3.已知对象中,Object引用.getClass()获取Class 对象引用

三、类型转型：
向上转型 显式
向下转型 SuperClass->SubClass

Class引用.cast() ->转为Class对象引用类型
Class引用.isInstance() ->动态 instanceof
判断：
instanceof isInstance 判断类型，类/派生类
equals == 只是判断实际的类是否一致，不考虑派生

四、反射调用

传统RTTI->对象具体类型，由编译决定
反射->基于构建的编程,RMI(远程方法调用)
区别：
RTTI 编译时打开和检查.class 文件
反射 运行时打开和检查.class文件
-----------------------------------------
1.default class 中Class 没有默认构造器，public class有默认构造器。
2.动态代理 Proxy.newProxyInstance 获取代理实例，需要实现InvocationHandler->内部method.invoke(Object,Object[]);（类和参数）

代理模式：对象+额外的操作

空对象
 
接口与类型信息： 

1.接口降低耦合->使用default class（让它无法强制转型)

2.
Method 
setAccessible(true)  调用有访问权限的方法

Method第二个参数     类型Class对象:int.class,String.class等

method.invoke()执行方法

{final基本类型反射无法修改：基本类型的静态常量，JAVA在编译的时候就会把代码中对此常量中引用的地方替换成相应常量值,通过反射修改域修饰符（modifiers值）。
f.getModifiers()值： 11010 == 26(注：private:2+static:8+final:16 = 26)} 

