---
layout: post
title:  "Java 정리"
comments: true
categories: devlog
tags: java
---

## JVM
  * 스택기반의 가상 머신
  * 메모리 관리, Garbage collection 수행

### 자바 프로그램 실행과정
  1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다.
    JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
  2. 자바 컴파일러가 자바 소스코드를 읽어들여 자바 바이트코드로 변환시킨다.
  3. Class Loader를 통해 class 파일들을 JVM으로 로딩한다.
  4. 로딩된 class 파일들은 Execution engine을 통해 해석된다.
  5. 해석된 바이트코드는 Runtime Data Areas에 배치되어 실질적인 수행이 이루어지게 된다. 이때 JVM은 필요에 따라 GC 같은 관리작업을 수행한다.

  * 자바는 동적코드, 런타임 때 참조

## Java 자료형
* Primitive type

type | byte | 범위
-----|---- | ---
byte | 1byte | -2^7~2^7-1(-128~127)
short | 2byte | -2^15~2^15-1(-32768 ~ 32767)
int | 4byte | -2^31~2^31-1(-2147483648~2147483647)
long | 8byte | -2^63~2^63-1
float | 4byte |
double | 8byte |
boolean | 1byte |
char | 2byte |

* Reference Type `java.lang.Object`
  * class
  * interface
  * Array
  * enum
  * etc.

</br>

## Wrapper class
  기본 자료형(Primitive data type)에 대한 클래스 표현을 Wrapper class라고 한다. `Integer`, `Float`, `Boolean` 등이 Wrapper class의 예이다. int를 Integer라는 객체로 감싸서 저장해야 하는 이유가 있을까? 일단 컬렉션에서 제네릭을 사용하기 위해서는 Wrapper class를 사용해줘야 한다. 또한 `null` 값을 반환해야만 하는 경우에는 return type을 Wrapper class로 지정하여 `null`을 반환하도록 할 수 있다. 하지만 이러한 상황을 제외한 일반적인 상황에서는 Wrapper class를 사용해야 하는 이유는 객체지향적인 프로그래밍을 위한 프로그래밍이 아니고서야 없다. 일단 해당 값을 비교할 때, Primitive data type인 경우에는 `==`로 바로 비교해줄 수 있다. 하지만 Wrapper class인 경우에는 `.intValue()` 메소드를 통해 해당 Wrapper class의 값을 가져와 비교해줘야 한다.

### AutoBoxing
  JDK 1.5 부터는 `AutoBoxing`과 `AutoUnBoxing`을 제공한다. 이 기능은 각 Wrapper class에 상응하는 Primitive data type일 경우에만 가능하다.

  ```java
  List<Integer> lists = new ArrayList<>();
  lists.add(1);
  ```
  우린 `Integer`라는 Wrapper class로 설정한 collection에 데이터를 add할 때 Integer 객체로 감싸서 넣지 않는다. 자바 내부에서 `AutoBoxing`해주기 때문이다.

  </br>


## Overriding vs Overloading
* 오버라이딩(Overriding) ~~riding 올라탄다~~
  상위 클래스에 존재하는 메소드를 하위 클래스에서 필요에 맞게 재정의하는 것을 의미한다.
* 오버로딩(Overloading)
  같은 클래스 내에 return value와 메소드명이 동일한 메소드를 매개변수만 다르게 만들어 다양한 상황에 메소드가 호출될 수 있도록 하는 것입니다.

</br>

## Access Modifier
  변수 또는 메소드의 접근 범위를 설정해주기 위해서 사용하는 Java의 예약어를 의미하며 총 네 가지 종류가 존재한다.

  * public  
    어떤 클래스에서라도 접근이 가능하다.

  * protected  
    클래스가 정의되어 있는 해당 패키지 내 그리고 해당 클래스를 상속받은 외부 패키지의 클래스에서 접근이 가능하다.

  * (default)  
    클래스가 정의되어 있는 해당 패키지 내에서만 접근이 가능하도록 접근 범위를 제한한다.

  * private  
    정의된 해당 클래스에서만 접근이 가능하도록 접근 범위를 제한한다.

    </br>


## Collection
  다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합
* List
  순서가 있는 데이터의 집합, `중복 허용 O`
* ArrayList
  단방향 포인터 구조, 자료에 대한 순차적 접근일 때 강점
  상당히 빠르고 크기를 마음대로 조절할 수 있는 배열
* Set  
  순서가 없는 데이터의 집합, `중복 허용 X`
  순서를 보장해주기 위해서는 `LinkedHashSet`을 사용한다.
* Map
  key-value로 이루어진 데이터의 집합, 순서 X, key 중복 허용 X, value 중복 허용 O
  key에 대해서 순서를 보장하기 위해서는 `LinkedHashMap`을 사용한다.

  * HashMap
    * key - value
    * 검색시 hasing
    * key - value 값으로 null 허용

* Stack과 Queue  
  `Stack` 객체는 직접 `new` 키워드로 사용할 수 있으며, `Queue` 인터페이스는 JDK 1.5부터 `LinkedList` 객체를 통해 `new`  키워드를 통해 사용할 수 있다. 자세한 부분은 DataStructure 부분의 설명을 참고하면 된다.

## Array, LinkedList
* LinkedList
  논리적 순서 순차 O, 물리적 순서 순차 X
  추가/삭제 유리, 검색 성능 고려 필요
  => 삽입, 삭제 빈번히 이루어질경우 용이

* Array
  논리적 순서 순차 O, 물리적 순서 순차 O
  검색 유리, 추가/삭제 성능 고려 필요
  ==> 이미 만든 구조에서 데이터의 접근만 하면 용이

* ArrayList
  Array와 비슷하나 동적인 길이

## Generic
제네릭은 자바에서 안정성을 맡고 있다고 할 수 있다.  다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에서 사용하는 것으로, 컴파일 과정에서 타입체크를 해주는 기능이다. 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안전성을 높이고 형변환의 번거로움이 줄어든다. 자연스럽게 코드도 더 간결해진다. 예를 들면, Collection에 특정 객체만 추가될 수 있도록, 또는 특정한 클래스의 특징을 갖고 있는 경우에만 추가될 수 있도록 하는 것이 제네릭이다. 이로 인한 장점은 collection 내부에서 들어온 값이 내가 원하는 값인지 별도의 로직처리를 구현할 필요가 없어진다. 또한 api를 설계하는데 있어서 보다 명확한 의사전달이 가능해진다.

## final keyword
* final class  
  다른 클래스에서 상속하지 못한다.

* final method  
  다른 메소드에서 오버라이딩하지 못한다.

* final variable  
  변하지 않는 상수값이 되어 새로 할당할 수 없는 변수가 된다.

추가적으로 혼동할 수 있는 두 가지를 추가해봤다.
* finally  
  `try-catch` or `try-catch-resource` 구문을 사용할 때, 정상적으로 작업을 한 경우와 에러가 발생했을 경우를 포함하여 마무리 해줘야하는 작업이 존재하는 경우에 해당하는 코드를 작성해주는 코드 블록이다.

* finalize()  
  keyword도 아니고 code block도 아닌 메소드이다. `GC`에 의해 호출되는 함수로 절대 호출해서는 안 되는 함수이다. `Object` 클래스에 정의되어 있으며 GC가 발생하는 시점이 불분명하기 때문에 해당 메소드가 실행된다는 보장이 없다. 또한 `finalize()` 메소드가 오버라이딩 되어 있으면 GC가 이루어질 때 바로 Garbage Collecting 되지 않는다. GC가 지연되면서 OOME(Out of Memory Exception)이 발생할 수 있다.

## 인터페이스 vs 추상클래스
* 인터페이스 `밑그림만 있는 기본설계도`
  구현 객체의 같은 동장을 보장하는 목적
  함수의 껍데기만 존재, 구현 클래스에 그 함수의 구현을 강제화 시킴
  클래스 X

* 추상클래스 `abstract` `미완성된 설계도, 클래스`
  추상 클래스를 상속받아 기능을 이용, 확장에 목적
  상속하는 클래스에게 구현을 강제화, 메서드 동작 구현을 자식에게 위임
  추상 클래스는 `추상 메소드`가 포함된 경우 or `abstract`로 정의된 경우

</br>

## Call by Value, Call by Reference
  기본형을 넘겨줄 경우 Call by Value가 발생하고 배열이나 클래스 객체 경우에는 Call by Reference가 발생한다. 자바는 모두 `Call by Value`이다. 레퍼런스 주소 값 또한 Call by Value로 복사되기 때문이다.

## 변수명
* 변수명은 숫자로 시작할 수 없다.
* _ 와 $ 문자 이외의 특수문자는 사용할 수 없다.
* 자바의 키워드는 변수명으로 사용할 수 없다. (예: int, class, return 등)

## 객체지향
  좀 더 나은 프로그램을 만들기 위한 프로그래밍 패러다임으로 로직을 상태(state)와 행위(behave)로 이루어진 객체로 만드는 것이다
  * 객체지향 5가지 원칙 `SOLID`
    * SRP : 단일 책임 원칙
      작성된 클래스는 하나의 기능만 가지며, 클래스가 제공하는 서비스는 하나의 책임을 수행하는데 집중되어야 한다

    * OCP : 개방 - 폐쇄 원칙
      소프트웨어의 구성요소(컴포넌트, 클래스, 모듈, 함수)는 확장에 열려있고, 변경에는 닫혀있어야 한다
      변경 비용은 줄이고, 확장 비용은 극대화해야함

    * LSP : 리스코프 치환 법칙
      자식 타입은 언제나 부모 타입들이 사용되는 곳에 교체할 수 있어야 한다

    * ISP : 인터페이스 분리 법칙
      자신이 사용하지 않는 메소드에 의존 관계를 맺지 말것
      어떤 객체의 사용자에게 필요한 메소드만 있는 인터페이스를 제공하라

    * DIP : 의존성 역전 법칙
      Dependency Inversion : 구조적 디자인에서 발생하던 하위 레벨 모듈 변경이 상위 레벨 모듈 변경을 요구하는 위계관계를 끊는 의미의 역전
      실제 사용 관계는 바뀌지 않고, 추상을 매개로 메시지를 주고 받아 관계를 최대한 느슨하게 만드는 원칙


## Serialization
* 직렬화 Serialization
  자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 byte 형태로 데이터 변환하는 기술
  * 자바 Primitive 타입과 `java.io.Serializable` 인터페이스 상속받은 객체
  * `java.io.ObjectOutputStream` 객체 이

* 역직렬화 Deserialization
  바이트로 변환된 데이터를 다시 객체로 변환하는 기술

## instanceof
  * 조상 참조변수 instanceof 자손 인스턴스
  * 만약 빈 자손 class를 만들면 자손 참조변수 instanceof 조상 인스턴스

## 파일입출력
  * FileInputStream 읽기

  * BufferedReader, FileReader 읽기
    * BufferedReader(new FileReader("c:/out.txt")) - readLine()

  * FileOutputStream 쓰기
    * getBytes()로 쓰기

  * FileWriter, PrintWriter 쓰기
    * FileWriter("c:/out.txt", true) - 추가모드(append) 열기
