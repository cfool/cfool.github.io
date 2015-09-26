---
layout: post
published: false
title: "HelloWorld"
author: "cfool"
description: ""
category: 
tags: [test, tag1]
---

    package main;

    class TestObject{
        private int a;
        private int b;
        
        public TestObject(int a, int b){
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
            TestObject other = (TestObject) obj;
            return a == other.a && b == other.b;
        }
        
    }

    public class Main {
        public static void main(String[] args) {
            
        }
    }
