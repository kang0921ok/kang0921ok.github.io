---
layout: default
title: 2. 코틀린 기초
parent: Kotlin In Action
grand_parent: Study
has_children: false
nav_order: 2
permalink: /docs/study/kotlin-in-action/2chapter
---

# 2장 코틀린 기초
- 2장에서는 변수(variable), 함수(function), 클래스(class)등을 확인하고 프로퍼티(property) 개념을 배운다
- 자바와 대략 비슷하나, 몇가지 중요한 개선에 다룰 예정
- 스마트 캐스트(smart cast)
    - 타입 검사 + 타입 캐스트 + 타입 강제 변환
- 예외 처리(Exception Handling)
- 단, 2장을 배운다고 코틀린다운 코드라고 부르긴 어렵다
- `kang tips!` 2장을 배우고 나면 leetcode를 코틀린으로 시도 해볼 수 있다

## 2.1 함수와 변수

### 2.1.1 Hello, World!
- ```kotlin
  fun main(args: Array<String>) {
      println("Hello, world!")
  }
  ```
- 함수 선언 시 fun keyword
- 파라미터 이름 뒤에 파라미터 타입 (변수도 동일)
- 함수를 최상위 수준에 정의 가능 (자바와 달리 꼭 클래스안에 함수 넣어야할 필요 없음)
- 배열 처리를 위한 문법이 따로 존재하지 않음 (?)
- 여러가지 표준 자바 라이브러리를 간결하게 사용할 수 있도록 wrapper 제공(e.g println())
- 세미클론 필요 없음

### 2.1.2 함수
- <img width="744" alt="스크린샷 2021-06-16 오전 9 29 31" src="https://user-images.githubusercontent.com/5463687/122140120-670fe800-ce85-11eb-9814-ba0b45377f5b.png">
- `if`는 코틀린에서 문장(statement)가 아닌 식(expression)
    - 식(expression)은 결과를 만들 수 있다
    - 코틀린은 루프를 제외한 대부분의 제어구조가 식(expression)
- ```kotlin
  fun max(a: Int, b: Int): Int = if (a > b) a else b
  ```
- 중괄호가 있는 경우 `블록이 본문`인 함수
- 등호와 식으로만 이루어진 함수를 `식이 본문`인 함수
- 코틀린에서는 식이 본문인 함수가 자주 사용 됨
- 반환 타입 생략도 가능
    - ```kotlin
      fun max(a: Int, b: Int) = if (a > b) a else b
      ```
    - 컴파일러가 본문식을 분석하여 함수 반환 타입을 정해줌
    - 다만 식이 본문일때만 가능하고 블록일때는 불가

### 2.1.3 변수
- val(value) = immutable
- var(variable) = mutable
- ```kotlin
  val question = "여러분은 행복한가요?"
  var answer = true
  // 3초 뒤
  answer = false
  // 3초 뒤
  answer = true
  
  question = "다시 한번 여러분은 행복한가요?" //val에 다시 값을 할당하고자 할 때 에러!
  
  val question2:String
  question2 = "다시 한번 여러분은 행복한가요?"
  ```
- 타입 생략 가능, 다만 초기화 식을 사용안하면 필수로 타입 지정 해야함
- 기본적으론 val 활용, 꼭 필요시에만 var 사용
    - 변경 불가능한 참조 + 변경 불가능한 객체를 부수효과가 없는 함수와 조합하면 함수형 코드에 가까워짐
    - val 사용 시 참조자체는 불변이지만, 참조내 객체 내부값 변경 가능
       - ```kotlin
         //이슈 없음
         val languages = arrayListOf("Java")
         languages.add("Kotlin")
         ```  

### 2.1.4 문자열 템플릿
- ```kotlin
  fun main(args:Array<String>) {
    val name = if(args.size > 0) args[0] else "Kotlin"
    println("Hello, ${name}!")
  }
  ```

- 변수 앞에 `$` 필수
- 중괄호를 빼는것도 가능하나, 안되는 케이스가 존재하여 넣는걸 추천(한글이슈, 배열값 사용)
- 컴파일시 존재 않는 변수 사용하면 에러
- `$`를 문자로 보고 싶으면 `\$` 

## 2.2 클래스와 프로퍼티
- ```java
  // 자바 Person class
  public class Person {
      private final String name;
      
      public Person(String name) {
          this.name = name;
      } 
      public String getName() {
          return name;
      }
  }
  ```
- ```kotlin
  // 코틀린 Person class
  class Person(val name : String)
  ```
- 코틀린의 경우 public이 default임으로 생략 가능

### 2.2.1 프로퍼티
- 클래스는 데이터를 캡슐화 하고 캡슐화한 데이터를 다루는 코드를 한 주체 아래에 가두는 것
- 자바에서는 데이터를 필드(field)에 저장하고 보통 비공개(private), 그리고 필드에 접근할 수 있는 접근자 메서드(accessor method, getter, setter) 제공
- 자바에서 `필드 + 접근자`를 묶어 `프로퍼티`라고 부름
- 코틀린은 이를 기본 제공
- ```kotlin
  class Person(
      val name : String,
      var age : Int
  )
  // name은 비공개 필드와 getter 만들어냄
  // age는 비공개 필드와 getter, setter 만들어냄
  ```
- `is`로 시작하는 프로퍼티는 get이 붙지 않는다
   - val isMarried : Boolean
   - person.isMarried -> 내부적으로 getter로 변환되어 호출 됨
   - person.isMarried() 
   - 자바는 is가 있어도 getIs 이런 형태로 변경됨
- 실제 코틀린에서 프로퍼티로 접근하여도 내부적으로는 getter로 변환되어 호출 됨

### 2.2.2 커스텀 접근자
- 프로퍼티의 접근자를 직접 작성하는 방법
- ```kotlin
  class Rectangle(val height: Int, val width : Int){
      val isSquare: Boolean
          get() { //프로퍼티 getter 선언
              return height == width
          }
          // get() = height == width // (이렇게도 선언 가능)
  }
  ```
- 위 코드에서 isSquare 프로퍼티에는 값을 저장하지 않고 게터만 존재

### 2.2.3 코틀린 소스코드 구조 : 디렉터리와 패키지
- 자바는 디렉터리 구조와 패키지 구조를 일치시켰음
- 코틀린은 강제하진 않음, 다만 왠만하면 디렉터리/패키지 구조 일치 시키면 된다
- 코틀린은 특히 여러 클래스를 한 파일에 넣는걸 주저할 필요 없다

## 2.3 선택 표현과 처리 : enum과 when
- ```kotlin
  //enum 선언
  enum class Color(
      val r: Int, val g: Int, val b : Int
  ) {
      RED(255,0,0),
      BLUE(0,0,255),
      GREEN(0,255,0),
      DARK(255,255,255),
      ORANGE(255,255,0);
  
      fun rgb() = (r * 256 + g) * 256 + b
  }
  
  println(Color.BLUE.rgb())
  ```
- ```kotlin
  //enum + when 활용
  fun getColorName(color : Color) =   
      when(color) {
          Color.RED -> "RED"
          Color.BLUE -> "BLUE"
          Color.GREEN -> "GREEN"
          Color.DARK, Color.ORANGE -> "ETC"
      }
  ```
- ```kotlin
  // 자바 switch는 분기조건에 상수만(enum, 숫자리터럴) 가능했으나 코틀린의 경우 임의의 객체도 허용
  fun mix(c1 : Color, c2 : Color) =   
      when (setOf(c1, c2)) {
          setOf(RED, YELLOW) -> ORANGE
          setOf(YELLOW, BLUE) -> GREEN
          setOf(BLUE, YELLOW) -> DARK
          else -> throw Exception("Dirty Color")
      }
  ```  
### 2.3.4 인자 없는 when 사용
- ```kotlin
  fun mix(c1 : Color, c2 : Color) =   
      when {
          c1 == RED && c2 == YELLOW -> ORANGE
          c1 == YELLOW && c2 == BLUE -> GREEN
          c1 == BLUE && c2 == YELLOW -> DARK
          else -> throw Exception("Dirty Color")
      }
  // 불필요한 가비지 객체 생성을 줄일 수 있긴함..
  ```    
### 2.3.5 스마트 캐스트 : 타입 검사와 타입 캐스트를 조합
- ```kotlin
  interface Expr
  class Num(val value:Int) : Expr
  class Sum(val left:Expr, val right:Expr) : Expr
  
  fun eval(e : Expr) : Int {
      if(e is Num) { //스마트캐스트, 마치 자바의 instanceOf, 캐스팅 없이 바로 사용 가능(컴파일러가 캐스팅 수행)
          return e.value  
      }
  } 
  ``` 
### 2.3.6 리팩터링 : if를 when으로 변경
- 코틀린은 3항연산자가 없다, if가 값을 만들어냄
- ```kotlin
  //if를 사용한 모습
  fun eval(e: Expr) : Int = 
      if(e is Num) {
          e.value
      } else if (e is Sum) {
          eval(e.right) + eval(e.left)
      } else {
          throw Exception("error")
      }
  ```  
- ```kotlin
  //if대신 when으로 변경 한 모습
  fun eval(e: Expr) : Int = 
      when(e) {
          is Num ->
              e.value
          is Sum ->
              eval(e.right) + eval(e.left)
          else ->
              throw Exception("error")
      }
  ```    
## 2.4 대상을 이터레이션 : while과 for 루프
- while
   - 코틀린과 자바 동일
- for
    - ```kotlin
      //for
      for(i in 1..100) {
          print(i)
      }
      
      for(i in 100 downTo 1 step 2) {
          print(i) // 2씩 줄면서 찍힘
      }
      ```      
- 맵 이터레이션
    - ```kotlin
      for(i in 'A'..'F') {
          print(i)
      }
      
      val map = TreeMap<Char, String>()
      for((key, value) in map) {
          print("$key : $value")
      }
      
      val list = arrayListOf("10","11","12")
      for((index, element) in list.withIndex()) {
          print("$index : $element")
      }
      ```  
- in으로 컬렉션이나 범위의 원소 검사
    - ```kotlin
      fun isLetter(c : Char) = c in 'a'..'z' || c in 'A'..'Z'
      fun isNotDigit(c : Char) = c !in '0'..'9' 
      ``` 
    - ```kotlin
      fun recognize(c : Char) = when(c) {
          in '0'..'9' -> "It's a digit"
          in 'a'..'z', in 'A'..'Z' -> "It's a letter"
          else -> "I don't know"
      }
      ```   
      
## 2.5 코틀린의 예외처리
- 코틀린에서는 checked, unchecked exception를 구분하지 않음
- 따라서, 자바와 다르게 함수 뒤에 `throws절`을 추가하지 않아도 된다. 
- try-catch-finally 동일
- try를 식으로 사용 가능
    - ```kotlin
      fun readNumber(reader: BufferedReader) {
          val number = try {
              Integer.parseInt(reader.readLine())
          } catch (e: NumberFormatException) {
              return
          }
      
          println(number) //exception 발생 시 위에서 이미 return되어 해당 로직 수행 안됨
      }
      
      fun readNumber(reader: BufferedReader) {
            val number = try {
                Integer.parseInt(reader.readLine())
            } catch (e: NumberFormatException) {
                null
            }
        
            println(number) //exception발생 시 null 찍힘
      }
      ```    

         
    