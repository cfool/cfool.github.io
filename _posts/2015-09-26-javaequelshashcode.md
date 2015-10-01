---
layout: post
title: "java重写equels时为什么要同时重写hashCode?"
author: cfool
description: ""
category: java
tags: []
---
在eclipse上，提供的重写equels方法的功能与重写hashCode的功能是放在一块的，为什么这两个通常必须要一块重写呢?   
在java api中，针对hashCode，有个常规协定：

* 在 Java 应用程序执行期间，在同一对象上多次调用 hashCode 方法时，必须一致地返回相同的整数，前提是对象上 equals 比较中所用的信息没有被修改。从某一应用程序的一次执行到同一应用程序的另一次执行，该整数无需保持一致。 
* 如果根据equals(Object)方法，两个对象是相等的，那么在两个对象中的每个对象上调用 hashCode 方法都必须生成相同的整数结果。 
* 以下情况不是必需的：如果根据 equals(java.lang.Object) 方法，两个对象不相等，那么在两个对象中的任一对象上调用 hashCode 方法必定会生成不同的整数结果。但是，程序员应该知道，为不相等的对象生成不同整数结果可以提高哈希表的性能。


*(详细参考[Java Api](http://docs.oracle.com/javase/7/docs/api/) Object类的hashCode方法介绍。)*   
在实际中，不同的jvm的默认hashCode方法实现方式不同，但是基本上对于不同的对象，返回的hashCode值一般是不相同的。所以，当我们只重写equals方法时，容易产生值相同的对象，hash值却不同的情况。这样与hashCode方法的常规协定是不相符的。这样会导致在很多用到hash值地方会产生错误。   
看下面的例子：

    import java.util.HashSet;
    import java.util.Set;

    class TestObject{
        private String flag;
        public TestObject(String flag){
            this.flag = flag;
        }
        public void show(){
            System.out.println("this is " + this.flag);
        }
    }

    class TestObjectA extends TestObject{
        private int a;
        private int b;
        
        public TestObjectA(int a, int b, String flag){
            super(flag);
            this.a = a;
            this.b = b;
        }

        @Override
        public boolean equals(Object obj) {
            if (this == obj)
                return true;
            if (obj == null)
                return false;
            if (getClass() != obj.getClass())
                return false;
            TestObjectA other = (TestObjectA) obj;
            return a == other.a && b == other.b;
        }
    }

    class TestObjectB extends TestObject{
        private int a;
        private int b;
        public TestObjectB(int a, int b, String flag){
            super(flag);
            this.a = a;
            this.b = b;
        }

        
        @Override
        public int hashCode() {
            final int prime = 31;
            int result = 1;
            result = prime * result + a;
            result = prime * result + b;
            return result;
        }

        @Override
        public boolean equals(Object obj) {
            if (this == obj)
                return true;
            if (obj == null)
                return false;
            if (getClass() != obj.getClass())
                return false;
            TestObjectB other = (TestObjectB) obj;
            return a == other.a && b == other.b;
        }
        
    }

    public class Main {
        public static void main(String[] args) {
            Set<TestObject> set = new HashSet<TestObject>();
            TestObjectA a1 = new TestObjectA(1,2, "a1");
            TestObjectA a2 = new TestObjectA(1,2, "a2");
            TestObjectB b1 = new TestObjectB(1,2, "b1");
            TestObjectB b2 = new TestObjectB(1,2, "b2");
            set.add(a1);
            set.add(a2);
            set.add(b1);
            set.add(b2);
            for (TestObject obj : set){
                obj.show();
            }
        }
    }

这一段代码产生的结果如下：

    this is b1
    this is a1
    this is a2

尽管a1.equals(a2)，但是由于a1与a2的hash值不相同，因此在HashSet的使用中，将这两个对象当成了不相等的对象，而b1和b2则被当成了相同的对象。   
_**所以，在重写equals的时候，一定记得要重写hashCode方法。**_

---------------------------------

参考资料：

* Ryan的cnblog <http://www.cnblogs.com/rcfeng/p/4030039.html>
* Java API <http://docs.oracle.com/javase/7/docs/api/>