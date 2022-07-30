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

## 😀 람다프로그래밍

#### 1. 람다 형태

{ x : Int , y : Int -> x+y }

#### 2. 람다식의 축약 과정

people 이라는 컬렉션(Person 객체들을 담은 리스트)에서 나이가 가장 큰 개체를 뽑아냄 , 이때 collection 에서 maxBy 함수를 사용    
maxBy 함수는 인자로 람다를 받는 함수임

- people.maxBy({ p: Person -> p.age})
    - 함수 호출 시 맨 뒤의 인자가 람다 식일 경우 람다를 괄호밖으로 뺄 수 있다.
- people.maxBy{ p: Person -> p.age}
    - 컴파일러가 자료형을 추론할 수 있다면 생략할 수 있다. maxBy 함수의 경우 파라미터의 타입은 항상 컬렉션 원소 타입과 같다
- people.maxBy{p.age}
    - 람다의 인자가 하나 뿐일 경우 이름을 붙이지 않아도 된다.
- people.maxBy{ it.age }

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



### 내부클래스와 중첩클래스
- 자바에서 클래스 내부에 클래스 구현시 기본적으로 내부클래스로 인식하고 바깥 클래스에 대한 참조를 저장한다.
- 자바에서는 내부 클래스에 static 을 붙여 중첩클래스로 만들어 참조를 저장하지 않을 수 있다.
- 코틀린 에서 클래스 내부에 클래스 구현시 기본적으로 중첩 인식하고 바깥 클래스에 대한 참조를 저장하지 않는다.
- inner 키워드를 추가하여 중첩클래스화 할 수 있다.

### 코틀린에서 기본을 중첩클래스로 변경한 이유
- 직렬화의 문제가 생길 수 있음
  - 내부 클래스의 직렬화를 진행할때 외부에 대한 참조로 직렬화 실패할 수 있음
- 원치 않는 참조로 인해 메모리 릭이 발생할 수 있음 또한 찾아내기 어려운 메모리 릭임

참고
- 리사이클러 뷰에서의 뷰홀더 사용시에도 중첩클래스나 top-level 의 선언을 고려하자
- 화면 사이즈 보다 많이 onCreateViewHolder 가 호출되어 뷰홀더들이 만들어지는데, Inner classes로 정의한다면 생성되는 객체마다 묵시적으로 Outer class를 항상 참조하게 된다
https://thdev.tech/kotlin/2020/11/17/kotlin_effective_11/

## by 키워드

- delegate 패턴을 통한 클래스 생성시 편리하다
- by 를 통해 인터페이스의 구현을 다른 객체에 위임할 수 있다.
- 오버라이드가 필요한 메서드만을 따로 구현해주면 된다.

## companion object (동반 객체)

- 동반객체를 감싸는 외부 클래스의 private 변수 및 함수에도 접근이 가능하다
  - 펙토리 패턴 구현에 매우 유리(생성자를 Private 하고 Companion object 를 통해 생성)
- 동반객체도 다른 싱글턴 객체와 마찬가지로 인터페이스를 구현할 수 있다.
- Java 의 static 키워드를 완전히 커버하며 그 이상의 기능을 제공




## 8장. lsit vs array

- array 는 원소는 바뀌고 크기는 불변
    - var arr = IntArray(size:10)
    - var arr = arrayOf(10,1)

### 제네릭

고정적인 자료형 대신 실제 자료형을 대체되는 **타입 패러미터**를 받아 사용하는 방법

- 장점 : generic 이 자료형을 대체하여 실제 자료형을 추론하고 캐스팅을 방지하여 성능을 높일 수 있다.

furn <T> genericFunc(var param:T){} -> genericFunc(1) 로 사용할 경우 자동으로 타입이 Int로 추론된다