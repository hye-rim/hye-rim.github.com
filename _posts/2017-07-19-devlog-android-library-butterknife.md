---
layout: post
title:  "안드로이드 라이브러리 사용하기 - 001.Butter Knife"
comments: true
subtitle:   "ButterKnife를 사용해보자"
categories: devlog
tags: android
---

![butterknifeLogo](https://github.com/JakeWharton/butterknife/raw/master/website/static/logo.png)  
~~버터가 먹고싶어지는 로고다~~

ButterKnife는 필드나 메소드가 안드로이드 뷰에 접근할 때 어노테이션(@)을 사용하여 더욱 편하게 접근하여 개발할 수 있도록 도와주는 라이브러리다.

먼저, Butter Knife를 사용하기 위해서는 build.gradle에 두줄만 추가하면 된다.

~~~java
GRADLE

compile 'com.jakewharton:butterknife:8.7.0'
annotationProcessor 'com.jakewharton:butterknife-compiler:8.7.0'
~~~

최신 버전을 기록했지만 업데이트 될 수 있으니 꼭 **공식 페이지에서 버전을 확인** 하는 것이 좋다.

* http://jakewharton.github.io/butterknife/

페이지 하단에 있다.
~~위에 있을 것 같아 한참 찾았다~~


 안드로이드 개발을 할 때 많이 사용하는 findViewById를 살펴보자. 평소에는 필요한 View를 사용하기 위해 선언을 한 뒤, 다시 findViewById를 호출했다. 만약 필요한 view가 많아질 경우 번거로움은 급격히 증가한다. 하지만 @BindView를 사용하면 이러한 번거로움을 줄일 수 있다.

**기존 방식**
~~~java
public class MainActivity extends BaseActivity {
  private final String TAG = MainActivity.class.getSimpleName();

  private EditText mInputEditText;
  private TextView mResultTextView;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    init();
  }

  private void init() {
    mInputEditText = (EditText) findViewById(R.id.main_input_editText);
    mResultTextView = (TextView) findViewById(R.id.main_result_editText);
  }
}
~~~

**Butter Knife**
~~~java
public class MainActivity extends BaseActivity {
  private final String TAG = MainActivity.class.getSimpleName();

  @BindView(R.id.main_input_editText) EditText mInputEditText;
  @BindView(R.id.main_result_editText) TextView mResultTextView;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ButterKnife.bind(this);
  }
}
~~~

자리를 차지하던 findViewById가 사라졌다 :)


Binding
-----
- - -  
**Activity**
~~~java
setContentView(R.layout.activity_main);
ButterKnife.bind(this);
~~~


**Fragment**
~~~java
View view = inflater.inflate(R.layout.fragment_sample, container, false);
ButterKnife.bind(this, view);
~~~

**View Holder**
~~~java
ButterKnife.bind(this, view);
~~~

이렇게 Activity, Fragment, Adapter 안의 ViewHolder에서도 사용가능하다.

추가적으로, Fragment의 경우엔 lifecycle이 Activity와 다르다. 효율적인 관리를 위해 onDestroyView에서 unbind해주는 것이 좋다.
~~~java
private Unbinder unbinder;

@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
  View view = inflater.inflate(R.layout.fragment_sample, container, false);
  unbinder = ButterKnife.bind(this, mView);

  return view;
}

@Override
public void onDestroyView() {
  super.onDestroyView();
  unbinder.unbind();
}

~~~


Listener Binding
-----
- - -  
이제 ClickListener의 경우를 살펴보자.
평소에는 setOnClickListener를 사용했지만 Butter Knife를 사용할 땐 필요없다.
그냥 바로 함수를 만든 뒤 @OnClick을 사용한다.

~~~java
@OnClick(R.id.main_send_button)
public void onClickSendButton() {
  ...
}
~~~

다수의 클릭 이벤트가 필요하다면 각각의 함수를 만들어도 되고 아래처럼 사용해도 된다.

~~~java
@OnClick({ R.id.first_button, R.id.second_button })
public void onClickButton(View view) {
  ...
}
~~~

ButterKnife는 유용한 라이브러리 중의 하나라고 생각한다. 혹시 다른 방법을 원한다면 데이터바인딩을 검색해보면 좋을 것 같다. :-)  



> onClick이 public이어야 하는 이유

> 특정 Activity나 View에 바인딩을 걸면 annotation이 부여된 모든 변수나 메소드에 대해 접근하려고 한다. 이때, ButterKnife 객체는 해당 클래스에 포함된 게 아니다. 그래서 private인 메소드는 바인딩 할 수 없다.


결론 : 열심히 공부해야겠다. 공부할게 넘쳐난다. 신난다!
