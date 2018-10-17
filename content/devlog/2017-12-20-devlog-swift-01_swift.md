---
layout: post
title:  "001.Swift란?"
comments: true
categories: devlog
date: 2017-12-20T17:10:20+09:00
draft: false
tags: swift
---

Swift란?
---------------------
- - -
Swift는 안전, 성능 및 소프트웨어 디자인 패턴에 대한 현대적인 접근 방식을 사용하여 만들어진 범용 프로그래밍 언어다. 또한 오픈 소스이다.


> 애플의 iOS와 OS X를 위한 프로그래밍 언어


![Alt text](https://developer.apple.com/swift/images/swift-og.png)  


기존의 애플 운영체제용 언어인 Objective-C와 함께 공존할 목적으로 만들어졌으며 Objective-C와 마찬가지로 LLVM으로 빌드되고 같은 런타임을 공유한다.

Swift는 개발자가 더 쉽게 작성하고 올바른 프로그램을 개발할 수 있도록 고안되었다. 그래서 입문자에게 보다 친숙하며, Scripting language 만큼 표현하기 쉬운 산업 품질 프로그래밍 언어이다.
~~industrial-quality programming language 해석한게 맞는지 모르겠다 :(~~

`Swift`의 몇 가지 추가 기능은 다음과 같다.

* 네임스페이스
* 제너릭스
* 튜플(tuple)을 활용한 다중 리턴 타입
* 클로저(closure)
* 타입 유추
* do, guard, defer, repeat 등을 사용한 고급 제어 흐름
* method, extension, protocol을 지원하는 구조체
* range, collection에서 빠르고 반복적인 반복
* 기능적 프로그래밍 패턴
* 강력한 오류 처리 내장
* 자동 관리되는 메모리
* 세미클론을 입력 할 필요 없다!

![Alt text](https://cnet1.cbsistatic.com/img/fiOkqm7EI8cWlAOxX0HLpbFZeZM=/fit-in/970x0/2014/06/03/a4efb219-8554-4402-9a40-3a13779a7e94/swift-c.jpg)  
*출처 : https://www.cnet.com/news/apples-swift-explained-what-it-is-and-what-it-means/*

Feature
-----
- - -
**Safe** 안정성  
Swift는 안전한 프로그래밍을 지향한다. 즉, 엄격한 문법을 통해 이를 지키고자 했다. 이것이 강제적이라고 느껴질 수 있지만 이는 실수를 줄이는 데 도움이 된다. 나중에 생길 쓸데없는 시간을 절약할 수 있다.


**Fast** 신속성  
Swift는 C 기반 언어(C, C++, Objective-C)를 대체하기 위한 용도로 만들어졌다. 성능을 예측 가능하고 일정한 수준으로 유지되는 것에 초점을 맞췄다.


**Expressive** 더 나은 표현성   
Swift는 최신 기능과 사용하기 쉬운 구문을 제공한다. 그러나 지금 버전의 Swift가 끝이 아니다. 지속적인 업데이트를 통해  개선하여 신속한 서비스를 개선 할 것이라 했다.


사용환경
-------
- - -
공식 지원 툴로는 Xcode에서의 Playground와 REPL이 있다.

**Xcode(Playground)**
![Alt text](http://is3.mzstatic.com/image/thumb/Purple117/v4/72/06/e7/7206e735-a957-ff3c-a706-fa69baf9c761/source/175x175bb.png)   
Xcode는 OS X 개발 툴 모음으로써 macOS에서 동작하는 통합 개발 환경이다. 이러한 Xcode의 기능으로써 Playground 있다.

![Alt text](https://i.ytimg.com/vi/zuBf8afPe6I/maxresdefault.jpg)  
Playground는 개발자가 Swift 코드를 즉시 테스트하고 결과를 확인할 수 있도록 도와준다.

**REPL**
![Alt text](https://cdn1.macworld.co.uk/cmsdata/features/3608274/Terminalicon2_thumb800.png)  
REPL은 Read-Eval-Pring Loop의 약자로 "읽기-실행-출력 반복"이라는 뜻이다. Swift는 이러한 REPL(Read-Eval-Print Loop)으로도 코드 실행이 가능하다. 이를 사용하기 위해서는 오픈 소스 스위프트 컴파일러가 설치된 리눅스나 맥에서 터미널을 실행하고 swift를 입력한다. 그럼 `swift REFL`이 실행된다.

**참고**  
* [swift 공식 홈페이지](https://swift.org/)  
* [swift 언어 개발 문서](http://swift.leantra.kr/#about-swift)  
* [swift 위키백과][swiftlink]
[swiftlink]: https://ko.wikipedia.org/wiki/%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4) "swift 위키백과"
