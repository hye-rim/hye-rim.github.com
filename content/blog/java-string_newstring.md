---
layout: post
title:  String, new String
date: 2017-12-19T17:10:20+09:00
draft: false
comments: true
subtitle:   "String 생성방식"
categories: blog
tags: java
---

**String, new String** - String 생성방식의 차이

~~~java
String a = new String("hello");
String b = new String("hello");
String c = "hello";
String d = "hello";

System.out.println(a==b); //case 1
System.out.println(c==d); //case 2
~~~

위 코드의 결과값은 어떻게 될까?
equals 메소드였다면 둘 다 true이다. 하지만 == 연산이므로 case 1은 `false`이고, case 2는 `true`이다.

- - - -
~~~java
String a = new String("hello");
String b = new String("hello");
~~~
a와 b는 heap 내에 일반적인 객체를 생성하게 되므로 **각기 다른 객체를 만들어 참조**한다. 그러므로 ==연산자의 결과가 `false`가 된다.

~~~java
String c = "hello";
String d = "hello";
~~~
그렇다면 c와 d는 **같은 객체를 참조**한다는 뜻이다. c가 선언되면 String constant pool에 "hello"가 저장될 것이고, d는 "hello"가 이미 있으므로 c와 같은 부분을 참조하게 된다. 그러므로 == 연산자의 결과는 `true`이다.

- - -
나는 주로 코드를 작성할 때 new String을 많이 쓰는데, 이럴 경우엔 호출될 때마다 항상 새로운 객체가 생성되므로 낭비가 된다. 그러므로 이 방법은 피하는 편이 좋고 아래처럼 사용하는 것이 좋다.

~~~java
String str = "hello";
~~~

앞으로 좀 더 신경 써서 개발해야겠다.
