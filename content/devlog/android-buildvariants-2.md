---
layout: post
title:  "[Gradle Build Variants] 다양한 버전의 앱 생성하기 - productFlavors"
comments: true
date: 2018-03-06T17:10:20+09:00
draft: false
categories: devlog
tags: android
---

이전 글에서는 build type을 달리 하는 법을 알아봤다면, 이번에는 여러 버전의 앱을 만들기 위해 gradle의 productFlavors 속성을 활용하는 법을 알아보겠습니다.

이 글에서 설정할 버전은 다음과 같습니다.
- 기존 버전의 full version 앱
- 앱의 크기가 커져서 가벼운 버전을 선호하는 사용자를 위한 lite version 앱
- 관리자를 위한 admin version 앱

>만약 buildType 속성을 활용해 debug, alpha, beta, release 등 build type을 달리 설정하는 방법이 궁금하시다면 아래의 이전 글을 참고해주세요.  
> [[Gradle Build Variants] 다양한 버전의 앱 생성하기 - buildType](https://hye-rim.github.io/devlog/2018/03/02/devlog-android-buildvariants-1/)

<br/>

#### productFlavors
----
- defaultConfig는 ProductFlavor의 클래스에 속하며 모든 버전에 대해 기본 구성을 제공합니다.(applicationId와 같은 모든 기본값 변경)
- applicationId, version code, version name 등 앱의 속성을 다르게 설정할 수 있습니다.
- 모듈별 **build.gradle** 스크립트에 `productFlavors` 속성을 추가하고 원하는 flavor을 추가합니다.
- flavorDimensions로 버전의 그룹명을 지정해주어야 합니다.(ex - "api", "mode")

아래 그림처럼 구현하기 위해 이전 글에 이어 `productFlavors`를 추가하겠습니다.
![buildtypes+productFlavors](/img/android/buildtypes+productflavors.png){: width="80%" height="80%"}
<br/>
~~~java
android {
    ...
    flavorDimensions 'version'
    productFlavors {
        main { //default
            dimension 'version'
        }

        lite {
            dimension 'version'
            applicationIdSuffix ".lite"
            versionNameSuffix "-lite"
        }

        admin {
            dimension 'version'
            applicationIdSuffix ".admin"
            versionNameSuffix "-admin"
        }
    }
}
~~~

<br/>

만약 여기서 `flavorDimensions` 이 없을 경우 아래와 같은 오류가 발생하게 됩니다.
![flavorDimensions_error](/img/android/flavorDimensions_error.png){: width="90%" height="90%"}

<br/>

applicationIdSuffix를 사용하게 되면 defaultConfig에 있는 applicationId 뒤에 추가로 붙게됩니다.
> lite version : com.test.lite

versionNameSuffix 또한 동일합니다.
> lite version apk : app-lite.apk

<br/><br/>

**Sync now** 를 누르게되면 Build Variant가 아래와 같이 바뀌게 됨을 볼 수 있습니다.

- Gradle은 빌드 유형과 제품 버전에 따라 자동으로 빌드 변형을 생성하고 product flavor, Build Type에 따라 빌드 변형의 이름을 지정합니다.

![buildvariant_set](/img/android/buildvariants-buildTypes+productFlavors.png){: width="300" height="300"}

<br/><br/>

#### 소스 세트 생성
-----

https://developer.android.com/studio/build/build-variants.html#sourcesets

1. Project 창을 열고 창 상단의 드롭다운 메뉴에서 Project 뷰를 선택합니다.
2. MyProject/app/src/로 이동합니다.
3. src 디렉토리를 마우스 오른쪽 버튼으로 클릭하고 New > Directory를 선택합니다.
4. applicationIdSuffix에 적은 값과 동일하게 적어준 뒤 OK를 클릭합니다.(ex - `lite` )
5. 생성한 디렉토리 안에 java/ 디렉토리를 생성합니다.

만약 추가로 다른 xml파일을 생성하고 싶다면,
1. 동일한 Project 창에서 src 디렉토리를 마우스 오른쪽 버튼으로 클릭하고 New > Android Resource Directory를 선택합니다.
2. Source Set 옆의 드롭다운 메뉴에서 해당 버전을 선택합니다.(ex - `lite` )
3. OK를 클릭합니다.

선택한 Build Variant 값에 따라 해당 버전이 활성화 됨을 볼 수 있습니다.

![buildvariants_src](/img/android/buildvariants-src.png){: width="60%" height="60%"}

---
만약, 소스 세트의 AndroidManifest.xml 파일들의 충돌로 apk 파일이 2개 생성 되는 등의 오류가 발생하면 다음 글을 참고해주세요 :)
~~제가 그랬거든요..ㅎㅎ~~
https://developer.android.com/studio/build/manifest-merge.html

>참고
>https://developer.android.com/studio/build/build-variants.html
>http://dktfrmaster.blogspot.kr/2016/10/gradle.html
