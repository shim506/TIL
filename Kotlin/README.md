# 기본 문법

## 1. 변수
- var , val 을 통해 변수를 선언한다.
- val 는 자바의 final 변수에 해당함 
- 선언 키워드 / 변수 이름 / 자료형 / 값 순으로 만듬
- 자료형은 값을 할당할경우 생략가능 (알아서 추론)

<br>

- ### val userName : String = "kildong"
- ### null 을 허용하는 변수에 대해서는 자료형 뒤에 ?를 추가한다.

<br> </br>
## 2. null 허용 변수에 대한 접근
<br>  null 가능성이 있는 변수에 대해서는 3가지 접근 방법이 존재함
1. 세이프 콜
    - 변수?. 을 통한 접근
    - null 검사를 하여 안전하게 호출하는 방법
2. non-null 단정
    - 변수!!. 을 통한 접근
    - 변수가 null이 아니라는 단정하에 접근 
    - null 일 경우  NPE 와 조우함
3. 엘비스 연산자
    - [str?.length ?: 값 ] 중 ?: 에 해당함
    - null 일 경우 값을 오른쪽 식을 실행함
    - ex) println("str1: ${str1?.length ?: 20}")

<br> </br>
## 3. 자료형
- 사용자는 모두 참조형 자료형으로 변수를 생성하고 JVM 에서 알아서 참조형과 원시형으로 변형한다.
- 변수 가능형 변수는 참조형으로서 힙에 저장된다. 
    - Int 와 Int? 는 == 은 true일 수 있지만 === 은 true 일 수 없음
    - 다만 byte 범위 안에 있다면 stack 이 아닌 cache에 저장되어 === true 가능
- "==" 연산자는 단순한 값 비교 , "===" 연산자는 주소값을 비교한다.
<br><br>


## 4. 함수
<br></br>
- 기본 함수 형태
```
// 기본형태
fun sum (a:Int , b:Int): Int{
    //표현식...
    return 반환값
}
```  
```
// 구현체를 '=' 으로 생략
fun sum : (a:Int , b:Int) ->Int = { x: Int , y : Int -> x*y}
```

```
// 구현체 '=' 으로 생략 + 반환형 자료형 생략
fun sum (a:Int , b:Int) = a +b
```
<br><br>
- 람다 함수 형태  
문장 속에 자료형을 충분히 추론할 수 있다면 맞는 방법일 가능성이 높다

```
// 람다식 함수를 매개 변수로 받는 고차 함수
result = hightOrder({x , y -> x + y} , 10 , 20)
```

```
// 람다식을 이용한 함수 - 생략 없는 기본형
val multi : (x : Int , y : Int) -> Int) = {x: Int , y:Int -> x * y}
```
```
// 매개변수의 타입생략
val multi : (Int , Int) -> Int = {x , y -> x*y }
```
```
// 변수의 타입 생략
val multi = {x: Int , y:Int -> x * y}
```

- 인자에 대한 기본값을 사용할 수 있다. (파이썬과 유사)
    - arg1:String , args:String ="default"

- 매개 변수 앞에 "vararg" 를 붙여서 가변인자를 사용할 수 있다.

<br><br>

### 4-1. 람다식


#### 형식
- value 처럼 다룰 수 있는 익명함수
- 두개이상의 입력을 한개로 단순화 한다는 개념  

#### 장점
1. 코드가 간결해짐
2. 다중 CPU를 활용하는 구조로서 병렬처리에 매우 용이

자료형 : (Int , Int) -> Int  
함수생성 : ={x: Int , y :Int -> x*y}

```
val square : (Int) -> (Int) ={number -> number*number}
```


### 4-2. 고차 함수와 람다식
고차함수는 인자나 반환값으로 함수를 사용함

### 4-3. 확장함수
```
fun 확장 대상.함수 이름(매개변수 , ...): 반환값{
    ...
    return 값
}
```

<br></br> 
## 5. 프로그램 흐름 제어
### 5.1 조건문
- when 조건문
```
   when(num){
        0 -> print("this is 0")
        1 -> print("this is 1")
        else -> print("this is else")
    }
```
```
   when(num){
        in 90..100 -> print("this is 0")
        in 10..80 -> print("this is 1")
        else -> print("this is else")
    }
```

<br><br>


## 6장. 클래스
- 주생성자의 동작은 init 을 통해 정의할 수 있다.
- 부생성자는 cunstructor로 생성하고 ,
- 클래스 매개 변수 할당을 다음과 같이 축약해서 작성할 수 있다.
```
class User(val id:Int, var name: String , var age: Int)
```
- getter 와 setter 는 자동 생성되고 val은 getter 만 생성된다.
- 커스텀 세터를 생성할때에는 'field'라는 예약어에 원하는 값을 넣는다.

## 8장. lsit vs array
- array 는 원소는 바뀌고 크기는 불변 
    - var arr = IntArray(size:10)
    - var arr = arrayOf(10,1)

