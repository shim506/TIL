# ✔ UI

## Android Id

- @+id
    - 해당 앱 내(자신의 apk내에서)새로운 resource Id를 생성함
- @android:id
    - 앱이 아닌 안드로이드 프레임워크에 있는 resource 에 접근함

## Constraint Layout - bias

- 일반적으로 anchor 를 양쪽으로 하면 중앙 정렬 된다.
- bias 를 설정하여 한쪽으로 치우치게 위치 시킬 수 있다.

## Layout Editor

### 미리보기 모양 변경

- 기기 유형별로 디자인을 미리 볼 수 있음
- 앱 테마별로 디자인을 미리 볼 수 있음
- ...

![img.png](img.png)

https://developer.android.com/studio/write/layout-editor?hl=ko

<br></br>

# ✔ 옵저버 패턴 및 리스너

- 인터페이스(리스너)를 연결다리로하여 발신객체의 이벤트를 수신객체에게 전달하는 것
- 발신 객체가 인자로 받거나 들고 있는 인터페이스 객체의 구현을 수신자에서 함으로 써 가능함

### 1. 둘사이를 이어줄 인터페이스(이하 리스너)

```
interface EventListener {
    fun onEvent(count: Int)
}
```

### 2. 발신자 객체

    - 발신자는 인자로서 리스너를 받는다.
    - 특정 이벤트 발생시 리스너의 함수를 실행한다.

### 3. 수신자 객체

- 리스너를 상속받아 리스너의 함수를 구현한다.

```

class EventPrinter : EventListener {
    override fun onEvent(count: Int) {
        print("${count}-")
    }
}
```

### 동작 과정

1. 발신자 객체에서 이벤트가 발생하면 생성시 인자로 넣은 인터페이스 함수를 실행한다.
2. 컴파일시 연결된 인터페이스 함수의 구현체로 이동하여(수신자) 원하는 동작을 실행하다.

## 안드로이드 button 클릭 분석

```
testButton.setOnClickListener(object: View.OnClickListener {
    override fun onClick(v: View?) {
        Toast.makeText(this, "버튼이 클릭되었습니다.", Toast.LENGTH_SHORT).show()
    }
})
```

- button 은 View 클래스를 상송받고 View는 setOnClickListener 함수를 갖는다.
- setOnClickListener 는 OnClickListener 인터페이스를 인자로 받고 OnClickListener 객체를 들고 있는다.
- button(View)가 클릭이 되면 안드로이드 내부적으로 performClick() 함수가 실행된다.
- performClick() 함수 는 내부적으로 OnClickListener 객체의 onClick 함수를 실행한다.
- 인터페이스 함수 onClick 을 구현한 내요을 실행하게 된다.

```
 public void setOnClickListener(@Nullable OnClickListener l) {
        if (!isClickable()) {
            setClickable(true);
        }
        getListenerInfo().mOnClickListener = l;
    }
```

```
public boolean performClick() {
    ...
    final ListenerInfo li = mListenerInfo;
    if (li != null && li.mOnClickListener != null) {
        li.mOnClickListener.onClick(this);
        ...
    } else {
        ...
    }
   ...
   }
```

## 리사이클러 뷰 적용

상황 : 리사이클러 뷰에 아이템이 선택 되면 액티비티에 특정 동작을 수행하게 한다.

- 어뎁터가 발신자
- 엑티비티 수신자

1. 리스너 인터페이스 생성 (어디 구현해도 ㄱㅊ)
2. 엑티비티에서 어뎁터에 인자로 리스너객체 넘기고
3. 어뎁터 클릭시 인터페이스 함수실행
4. 엑티비티에서 리스너 객체 구현

# ✔ ViewBinding

- findViewById 를 대체하여 사용할 수 있다.

viewBinding은 gradle에 설정하는 것 만으로 개발자가 작성한 레이아웃 파일들을 다음과 같은 공식으로 모두 바인딩클래스로 자동변환 해줍니다.

자동변환공식 : 레이아웃파일명(첫 글자와 언더바 다음영문을 대문자로 변환) + Binding 예)
activity_main.xml = ActivityMainBinding activity_sub.xml = ActivitySubBinding item_recycler.xml = ItemRecyclerBinding

# ✔인텐트

- 4대 컴포넌트들끼리 정보를 전달할 수 있게 해주는 매세징 객체이다.
- 구성 요소로 Action 과 Data 등이 있다.
- 두종류의 명시적 , 암시적 인텐트로 나뉜다.

## 1. 명시적 & 암시적 인텐트

### 명시적 인텐트

- 클래스 객체나 컴포넌트 이름을 지정해서 호출할 대상을 아는 경우
- 앱 내부에서 사용함

### 암시적 인텐트

- 액션과 데이터를 지정했지만 호출 대상이 달라질 수 있는 경우
- 앱 외부 통신할 때 사용함
- 설치된 앱 정보를 알고있는 안드로이드 OS가 인텐트에 맞는 적절한 앱의 컴포넌트를 찾고 사용자에게 대상과 처리 결과를 반환

## 2.인텐트 필터

- 매니패스트 파일에 존재함
- 확성기로 뿌려진 인텐트를 잡아낼 필터
    - 다른 앱의 특정 인텐트에 대해 응답 하고 싶다면 인텐트 필터에 명시해준다. .

![img_1.png](img_1.png)

## 3. 인텐트 구성요소

### Action

- 인텐트를 대표하는 값
- 1개의 액션만을 가질 수 있음
- 인텐트의 Action 을 최우선적으로 고려하여 앱들의 인텐트 필터 내용 중 가장 적합한 컴포넌트 들을 채택함

```
public static final String ACTION_VIEW = "android.intent.action.VIEW";
public static final String ACTION_CALL = "android.intent.action.CALL";
```

### Category

- 리졸빙 두번째 고려 속성
- Action 과 다르게 여러개 가능

### Data

- URI 를 말한다.
- intent.setData(uri) 추가
- intent.data 로 접근

### MIME Type

- 데이터 타입을 표시
- intent.setType("video/mp4")

## 리졸빙

- 인텐트 필터를 기준으로 인텐트에 맞는 컴포넌트를 찾는 과정
- intent를 보내는 앱의 PackageManager 는 디바이스 모든앱의 인텐트 필터를 검사해서 유사도를 파악하여 수치화한다.



 