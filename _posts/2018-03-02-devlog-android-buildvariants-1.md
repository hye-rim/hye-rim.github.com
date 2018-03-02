---
layout: post
title:  "[Gradle Build Variants] 다양한 버전의 앱 생성하기 - 1"
comments: true
categories: devlog
tags: android
---

앱을 개발하다 보면 한가지 버전의 앱만으로는 아쉬울 때가 종종 있습니다. 예를 들어
- 광고의 여부에 따라 free/paid version 앱
- 앱의 크기가 커져서 가벼운 버전을 선호하는 사용자를 위한 lite version 앱
- 관리자를 위한 admin version 앱

그냥 별 고민하지 않고 만든다면 아마 프로젝트를 복사하여 여러 개의 프로젝트를 생성할 것입니다. 이렇게 되면 수정/추가해야 할 사항이 있다면 모든 프로젝트를 수정해야 하고, 같은 부분임에도 코드가 다른 경우가 발생할 것입니다.

또한, 개발 서버와 릴리즈 서버가 구분되어 있을 경우 상황에 따라 서버 부분 코드를 계속 바꿔줘야 합니다. 상상만 해도 복잡해지지 않나요?

이럴 때 gradle의 `buildType`과 `productFlavors`를 활용하면 편해집니다 :)


gradle은 하나의 프로젝트에서 다양한 버전의 앱을 생성할 수 있도록 도와줍니다.


#### Build Type
---
- 앱의 개발 과정에 따라 나눌 수 있습니다. (`debug`, `alpha`, `beta`, `release` 등)
- build type에 따라 프로가드 적용 여부, 디버그모드 허용 여부 등을 각기 설정할 수 있습니다.
- 모듈별 **build.gradle** 스크립트에 `buildTypes` 속성을 추가하고 원하는 build type을 추가합니다.

- build type을 debug, alpha, beta, release로 설정한 코드입니다.
~~~java
android {
    ...
    buildTypes {
      debug {
          applicationIdSuffix ".debug"
          minifyEnabled false
          debuggable true
          proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
      }
      alpha {
          applicationIdSuffix ".alpha"
          minifyEnabled false
          debuggable true
          proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
      }
      beta {
          applicationIdSuffix ".beta"
          minifyEnabled true
          debuggable false
          proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
      }
      release {
          applicationIdSuffix ".release"
          minifyEnabled true
          debuggable false
          proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
      }
  }
}
~~~

아래 그림처럼 **Build Variant** 에서 변경할 수 있습니다.

![buildvariant_build_type](/assets/img/android/buildvariants-buildTypes.png){: width="300" height="300"}

<br/>
<br/>
만약 개발 서버와 릴리즈 서버가 구분되어 있으면 `buildConfigField`를 활용합니다.

![buildtypes-api_server](/assets//img/android/buildTypes-api_server.png){: width="80%" height="80%"}

~~~java
android {
    ...
    buildTypes {
      debug {
          ...
          buildConfigField "boolean", "IS_DEBUG", "true"
      }
      release {
          ...
          buildConfigField "boolean", "IS_DEBUG", "false"
      }
  }
}
~~~
<br/>
위와 같이 선언하면 소스코드에서 아래와 같이 사용할 수 있습니다.
<br/>

~~~java
private Retrofit getRetrofitSetting() {
    ...
    if (BuildConfig.IS_DEBUG) {
        //개발 서버 연결
    } else {
        //릴리즈 서버 연결
    }
}
~~~
<br/>
<br/>
<br/>

다음 포스팅에서는 아래 그림처럼 구현하기 위해 productFlavors를 추가로 알아보겠습니다.

![buildtypes+productFlavors](/assets/img/android/buildtypes+productflavors.png){: width="80%" height="80%"}




>참고
https://developer.android.com/studio/build/build-variants.html
http://gun0912.tistory.com/74
