# Kotlin 개념

## 목차
- [변수 선언](#변수-선언)
- [정적 ˙ 동적 타입 언어](#정적-˙-동적-타입-언어)
- [if, else, when](#if-else-when)
- [반복문](#반복문)
- [함수](#함수)
- [Kotlin 함수를 Java에서 쓰기](#Kotlin-함수를-Java에서-쓰기)
- [함수의 파라미터](#함수의-파라미터)
- [Getter, Setter](#Getter-Setter)
- [프로퍼티(Property)와 필드(Field)](#프로퍼티(Property)와-필드(Field))
- [상속](#상속)
- [클래스 위임](#클래스-위임)
- [프로퍼티 위임](#프로퍼티-위임)
- [내부 클래스와 중첩 클래스](#내부-클래스와-중첩-클래스)
- [Collectioin의 함수형 API](#collectioin의-함수형-api)
- [확장 함수](#확장-함수)
- [널 안정성(Null Safety)](#널-안정성(null-safety))
- [Object](#object)
- [Companion Object](#companion-object)
- [Coroutine](#coroutine)

## 변수 선언
1. val
    - 변경 불가능한 참조를 저장하는 변수(Value)
    - val로 선언하면 초기화 이후 '변수의 재 대입'이 불가
    - Java에서 'final' 키워드로 선언하는 것과 같음
2. var
    - 변경 가능한 참조(Variable)
    - Java의 일반적인 변수에 해당
3. lateinit
    - ```kotlin
      // 예제
    
      // lateinit을 안 사용하면
      // null이 가능한 변수로 선언
      private var str : String? = null
      // 이렇게 만들면 null이 가능하기 때문에
      // 계속해서 null check를 해줘야 함
      str = "Hello World"

      // lateinit을 사용하면
      // null이 될 수 없는 변수로 선언됨
      private lateinit var num : Int
      // null check를 안 해줘도 됨
      num = 10

      // lateinit을 사용하려면 타입이 꼭 'var'여야 함
      ```


## 정적 ˙ 동적 타입 언어
1. 정적 타입 언어
    - 컴파일 시에 타입이 결정
    - 컴파일 시에 타입 캐스팅 문제를 확인할 수 있음
    - 실행이 빠름
    - 반드시 변수를 선언할 때 타입을 적어야 하므로  
    코드 작성 시에 타입을 신경 써야 함
    - 코틀린
2. 동적 타입 언어
    - 프로그램 실행(런타임) 시에 타입을 결정
    - 변수의 타입에 상관없이 코딩하기 때문에 코드 작성이 쉬움
    - 사전에 타입을 체크하지 않기 때문에 프로그램 실행 중  
    타입으로 인한 에러가 발생할 수 있음

## if, else, when
- if, else의 사용법은 Java와 같음
```kotlin
// 예시
when(numberEx) {
    1 -> println("1번 출력")
    2 -> {
        println("2번 출력")
    }
    // numberEx가 3 ~ 6까지인 경우 실행
    in 3..6 -> println("3 ~ 6번 출력")
    7, 9 -> {
        println("7, 9번 출력")
    }
    else -> println("나머지 출력")
}
```

## 반복문
- while과 do ~ while, continue의 사용법은 Java와 같음
```kotlin
// 예시

// collection의 길이만큼 실행, item이 하나하나에 해당됨
val array: Array<String> = arrayOf("a", "b", "c")
for(item in array) {
    println(item)
}

// 특정 숫자값을 반복
for(i in 1..10) {
    println(i)
}

// 인덱스(순서)가 필요한 경우
val collection = mutableList<String>("a", "b", "c")
for((index, value) in collection.withIndex()) {
    println("${index} : ${value}")
}

// break를 사용할 때 어디까지가 반복인지 알기 쉽게 해줌(마킹과 같은 개념)
loop1@ while(true) {
    var x = retrieveData()
    if(x == null) break@loop1
    else {
        loop2@ while(true) {
            var y = getData()
            if(y == null) break@loop2
        }
    }
}
```

## 함수
```kotlin
// 예시

// Java
// public void function1() { }
fun function1() {} // void와 같은 형태로 Unit 타입이 있지만 생략 가능

// Java
// public void function2(int i) { }
fun function2(i: int) { }

// Java
// public int function3(int i) { return 0; }
fun function3(i: int): int { return 0 }
```

## Kotlin 함수를 Java에서 쓰기
- 가장 상단에 `@file:JvmName(Java에서 쓸 이름)`으로 사용
- Java에서 클래스 안에 함수를 사용하듯이 사용

## 함수의 파라미터
```kotlin
// 예시

// 함수의 파라미터의 기본값을 설정 가능
fun toast(message: String, length: Int = Toast.LENGTH_SHORT) {
    Toast.makeText(applicationContext, message, length).show()
}

// 파라미터의 이름을 써 지정한 파라미터값만 변경 가능
fun printText(p1: int, p2: int = 2, p3: int) {
    println(p1 + p2 + p3)
}
printText(p1 = 1, p3 = 3)
```

## Getter, Setter
```kotlin
class Person {
    // Getter와 Setter를 기본적으로 지원

    // var로 선언된 변수는 Getter와 Setter 전부 생성
    var age: Int = 0
    // val로 선언된 변수는 Getter만 생성
    val name: String
    // 생성자에서 이름을 받음(생성자 부분)
    constructor(name: String) {
        this.name = name
    }
}

// constructor 대신 이름 옆에 써도 가능
class Person2(val name: String) {
    var age: Int = 0
}
```
```kotlin
class Person(val name: String) {
    var age: Int = 0

    // 전달된 값을 그대로 사용하지 않을 때(자동으로 생성된 Setter로는 안 됨)
    var nickname: String = ""
        set(value) {
            // field는 Setter의 대상이 되는 field를 의미
            // field는 Setter 메소드 내의 '값을 적용할 영역'을 의미
            // field 대신 this.nickname을 사용하면 setNickname()을 호출해 재귀호출이 됨
            field = value.toLowerCase()

            // custom Setter(set(value))에서는 필드에 접근하고자 위 코드같이  
            // field 키워드로 접근했으므로 Backing Field
            // Backing Field는 프로퍼티를 뒷받침하는 필드라는 의미  
            // (클래스 내부의 접근자에서만 사용 가능)
        }
    
    // Java
    // public void setNickname(String nickname) {
    //     this.nickname = nickname.toLowerCase();
    // }
}
```

## 프로퍼티(Property)와 필드(Field)
1. 필드(Field)
    - 클래스에 선언되어 있는, `클래스 변수`가 아닌 `인스턴스 변수`를 의미
    - 필드는 외부에서 접근할 수 있는 Getter, Setter 메소드가 반드시 존재할 필요 X
    - 코틀린은 기본적으로 필드를 사용하지 않음
    ```java
    // Java
    public class FieldJava {
        // 인스턴스에서 사용하는 변수이므로 Field
        public int field1;

        // 접근 제어자와 상관없이 모두 Field
        private double field2;
        protected String field3;

        // Getter, Setter가 있어도 Field
        private int field4;

        public int getField4() { return field4; }
        public void setField4(int field4) { this.field4 = field4; }

        // 클래스 변수는 Field가 아님
        static int notField1;

        void func1() {
            // 함수 내의 변수들은 Field가 아닌 지역변수
            int notField2 = 0;
        }
    }
    ```
2. 프로퍼티(Property)
    - 필드(Field)와 외부에서 접근 가능한 Getter 또는 Setter가 있는 경우  
    -> 필드(Field)와 접근 가능한 Getter, Setter의 조합
    - 코틀린은 Getter와 Setter가 자동으로 생성되므로 Property
    - 코틀린은 Field를 사용하지 않음
    ```java
    // Java
    public class PropertyJava() {
        // Field가 선언되어 있고 Getter, Setter가 있는 경우 Property
        private int property1 = 0;

        public int getProperty1() { return property1; }
        public void setProperty1(int property1) { this.property1 = property1; }

        // 변수의 값을 읽을수만 있는 경우도 Property라 할 수 있음
        private property2 = "";

        public String getProperty2() { return property2; }

        // 단순 Field는 Property가 아님
        private int notProperty1 = 0;

        // 클래스 변수 역시 property가 아님
        private static int notProperty2;
    }
    ```

## 상속
- 상속은 `2가지 측면으로 접근 가능`, `코드 구현애 대한 상속`과 `인터페이스 집합에 대한 상속`
- 코틀린의 클래스는 `기본적으로 상속이 불가`
1. 코드 구현의 상속 = 코드의 복사와 붙여넣기를 줄여 주는 역할
```java
public class Foo {
    int field1 = 0;

    public int getField1() { return field1; }
    public void setField1(int field1) { this.field1 = field1; }
}

// extends 키워드로 상속 받은 경우 코드의 구현을 상속 받는 것이 됨

public class Bar extends Foo {
    int field1 = 0;

    public int getField1() { return field1; }
    public void setField1(int field1) { this.field1 = field1; }
}
```
2. 인터페이스 상속 = 코드 구현이 아닌 메소드의 집합을 상속받음
    - 인터페이스를 사용하는 객체에서 인터페이스에 정의한 코드를 신경 쓰지 않고 호출할 수 있도록 하는 데에 의의가 있음

3. 취약한 기반 클래스 문제(fragile base class)
    - 하위 클래스에서 상위 클래스의 메소드를 오버라이딩하면서 발생
    - 클래스를 사용하는 코드에서는 클래스의 실제 구현에는 관심을 가지지 않아야 하기 때문에 발생
    ```java
    // 예시

    // 이동 가능한 객체를 클래스화
    public class MoveObject {
        // 이동 스피드
        protected int speed;

        public void addSpeed(int param) {
            this.speed = speed + param;
        }

        public int getSpeed() { return speed; }

        // 좌표
        public int x, y;
    }

    /* MoveObject가 선언한 x, y좌표 속성은 필요하지만, 이동 속도는 항상 '0'인 새 오브젝트가 필요해져서 코드를 재사용하기 위해 CantMoveObject를 MoveObject의 상속을 받아 만들었다고 가정 */

    public class CantMoveObject extends MoveObject {
        // 생성자에서 speed를 0으로 만듬
        public CantMoveObject() { this.speed = 0; }

        // addSpeed 메소드를 오버라이드
        @Override
        public void addSpeed(int param) {
            // 움직일 수 없는 오브젝트이므로 아무것도 하지 않음
        }
    }

    // 위에 상속은 객체 지향의 주요 개념을 위반함
    public class Calculator {
        // 명중률 계산 함수, 파라미터로 MoveObject 객체와 공격자의 명중률을 받음
        public static int calcAccuracy(MoveObject moveObject, int attackerAccuracy) {
            // moveObject의 speed가 0인 경우 잘못된 상황으로 판단하여 스피드 1을 추가
            if(moveObject.getSpeed() == 0) {
                moveObject.addSpeed(1);
            }

            // 위의 코드로 moveObject.getSpeed()가 0이 나오지 않는다고 나눗셈을 함
            double resultAccuracy = attackerAccuracy / moveObject.getSpeed();
            return (int) resultAccuracy;
        }
    }

    /* 위의 클래스는 calcAccuracy() 함수에서 moveObject의 스피드가 '0'인 경우 뭔가가 잘못되어 꼬인 상황으로 판단하고 'moveObject.addSpeed()' 함수로 속도를 '1'로 만듬. 이 경우 MoveObject 클래스만 있는 경우에는 문제가 되지 않지만 MoveObject가 사실 'CantMoveObject'라면 '0'값을 나누게 되어 에러가 발생 */

    /* 한 번은 MoveObject의 실제 인스턴스를  MoveObject 클래스로 하고 다음에는 CantMoveObject로 하고 있음. MoveObject를 사용하는 Calcurator 입장에서는 MoveObject가 실제로는 어느 클래스인지 상관없이 사용할 수 있어야 함. 그런데 상속으로 오버라이딩을 하면서 Calcurator는 MoveObject가 실제로 어떤 클래스인지 알 수 없어 에러 발생  
    -> 객체 지향의 주요 원칙인 캡슐화의 주요 목적 중 하나는 클래스를 사용하는 측면에서 해당 클래스의 구체적인 사항을 모르게 하는 것. 하지만 구체적인 구현 클래스를 알아야만 하므로 캡슐화가 깨졌다고 볼 수 있음 */
    ```

4. 상속을 금지
- Java분야에서 유명한 책인 'Effective Java'에서 `상속을 위한 설계와 문서를 갖추거나, 그렇지 않은 경우 상속을 금지하라`라고 함.  
(상속 = 코드의 구현을 상속받는 경우)
- Java에 경우 금지하는 방법은 메소드나 클래스 앞에 final을 쓰면 됨.
- 코틀린은 기본적으로 상속이 불가능함.  
하지만 클래스나 메소드 앞에 `open`을 사용하면 상속 가능

확장 함수, 널 안정성 추가 

## 클래스 위임
- 객체 지향에서 위임 = 클래스의 특정 기능들을 대신 처리해 주는 것
- 위임을 사용하는 대표적인 패턴은 데코레이터(Decorator) 패턴
- 데코레이터 패턴 = 특정 클래스의 기능에 추가 기능을 덧붙이는 방법
```java
// 예제

// 캐릭터에 장학을 하면 '검의 이름으로 장착되었다'는 메세지를 출력하는 클래스

// 검 객체 클래스
public final class Sword {
    // 검의 이름
    String name;

    // 생성자에서 이름을 받음
    public Sword(String name) { this.name = name; }

    // 장착 시 불리는 메소드
    public void equip() { System.out.println(name + " 이 장착되었다."); }
}

// 마법검일 때는 다른 사운드가 추가되게 하고 싶어함.
// 하지만 final로 인해 상속이 불가능한 상태일 때 데코레이터 패턴을 사용
// 아래와 같이 Sword 클래스의 메소드를 전부 포함하는 인터페이스 제작

public interface ISword {
    // 장착 시 불리는 메소드
    void equip();
}

// 그 후 기존의 Sword 클래스에 다음과 같이 인터페이스만 상속

public final class Sword implements ISword {
    // 검의 이름
    String name;

    // 생성자에서 이름을 받음
    public Sword(String name) { this.name = name; }

    // 장착 시 불리는 메소드
    public void equip() { System.out.println(name + " 이 장착되었다."); }
}

// 이제 Sword 클래스는 상속을 하지 않고도 기능 확장할 수 있는 밑준비가 끝남.
// 아래는 마법검에 해당하는 클래스

// ISword 인터페이스를 상속받음
public class MagicSwordDelegate implements ISword {
    // ISword 타입의 객체를 필드로 가지고 있음
    // 단지 Sword 클래스를 확장하려면 Sword 타입으로 해도 되지만 
    // ISword 타입으로 하면 확장성이 더욱 증가
    ISword iSword;

    // 생성자에서 ISword 타입의 객체를 생성자에서 받음
    public MagicSwordDelegate(ISword iSword) {
        this.iSword = iSword;
    }
    // 확장 기능을 실행한 뒤 필드로 가지고 있는 iSword 클래스의 equip() 함수를 호출
    // 아래와 같이 '기존에 설계된 객체에게 책임을 전달하는 것'이 위임

    // 장착 시 불리는 메소드
    @Oevrride
    public void equip() {
        // 멋진 사운드를 플레이한다.
        playWonderfulSound();

        // 기존 기능은 iSword에 위임
        iSword.equip();
    }

    // 확장기능 - 멋진 사운드를 플레이하는 메소드
    public void playWonderfunSwound() {
        // 멋진 사운드를 플레이
        System.out.println("짜잔");
    }
}

// 위 클래스는 ISword 인터페이스를 필드로 가지고 있음.
// 단지 Sword 클래스의 기능에 추가 기능을 덧붙이는 경우면 Sword 타입을 필드로 가져도 상관없지만
// 인터페이스를 필드로 가지면 이후 인터페이스를 상속받은 모든 클래스에 대하여 확장 기능 사용 가능
```

## 프로퍼티 위임
- 코틀린은 클래스와 프로퍼티 위임 제공  
프로퍼티 위임은 Getter, Setter 연산자를 위임할 수 있게 하고, 3가지 방법을 제공
    1. lazy properties = 값의 초기화를 처음 프로퍼티를 사용할 때 초기화
    2. observable properties = 프로퍼티에 값이 변경되면 옵저버에 알려줌
    3. storing properties = 필드가 아닌 맵에 속성을 저장

```kotlin
// 예제

// 프로퍼티에 Getter, Setter를 위임하는 방법
// 코틀린은 Custom Getter, Setter를 활용해 자동으로 생성되는 Getter, Setter를 변경할 수 있지만
// 종종 여러 클래스에서 같은 동작을 해야 할 경우가 있을 수도 있음
// (String 문자열 프로퍼티의 Setter가 호출될 때 자동으로 문자열을 대문자로 변경해야 하는 경우)
// 그 때 위임을 사용하면 편리함

class DelegateString {
    // Setter에서 호출된 값을 저장할 변수
    var text = ""

    // operator는 연산자를 의미
    // 붙인 이뉴는 Getter, Setter 메소드가 연산자로 취급되기 때문에
    operator fun getValue(thisRef: Any?, property: KProperty<*>): String {
        return text
    }

    operator fun setValue(thisRef: Any, property: KProperty<*>, value: String) {
        // 대문자로 변경하여 저장
        text = value.toUpperCase()
        // Setter에 호출될 때의 문자열과 변경 후 문자열을 프린트
        println("$value ==> ${text}")
    }
}

// 이제 어디서든 위임 클래스를 사용 가능
class User {
    // 닉네임은 DelegateString클래스에 위임
    var nickname by DelegateString()
}

// User 클래스는 nickname이라는 속성(property)이 있는데 이것은 DelegateString에 위임됨
// 이게 가능한 이유는 코틀린에서 속성(property)은 Field로 정해지는 것이 아니라 
// 접근자인 Getter, Setter에 의해 결정되기 때문
// 프로퍼티 위임 클래스에 요구사항으로는 var 선언된 변수는 getValue, setValue 둘 다 구현
// 하지만 val 선언된 변수는 getValue만 있어야 함
```
1. lazy 위임
    - 프로퍼티의 초기화를 인스턴스 생성 시점이 아니라 프로퍼티를 사용하는 시점에 초기화
    - 초기화가 오래 걸리는 속성이 있는 경우, 인스턴스 생성 시점에 모든 초기화를 진행한다면 전체적인 성능이 매우 저하됨
    - 따라서 초기화를 하지 않고 사용하다가 실제로 사용하는 시점에 초기화를 함
    ```kotlin
    // 예제

    // 위의 코드를 수정

    class User {
        // 닉네임은 DelegateString 클래스에 위임
        var nickname by DelegateString()

        // lazy 위임은 val 키워드로 선언되어야만 가능함
        // 네트워크에서 받은 텍스트는 시간이 걸리므로 실제로 사용할 때 초기화
        val httpText by lazy {
            println("lazy init start")
            InputStreamReader(URL("http://www.naver.com").openConnection()).readText()
        }
    }

    // User 클래스의 httpText는 네트워크에서 데이터를 읽어야 초기화.
    // 보통 네트워크에서 데이터를 읽어 오는 경우 속도가 매우 느려짐
    // 이런 경우 인스턴스 생성 시점 httpText의 초기화가 진행되면 실제로는 
    // httpText를 사용하지 않는다고 해도 초기화가 느려짐
    // 약간 비동기 느낌
    ```

2. observable 위임
    - `옵저버`를 사용하는 패턴은 주로 관찰하고자 하는 대상에 변경 사항이 생길 때,  
    변경된 사실을 관측자에게 알려 주는 것, 여기서 관찰 대상은 프로퍼티
    ```kotlin
    // 예제

    // 위의 코드를 수정

    class User {
        // 닉네임은 DelegateString클래스에 위임 O
        var nickname by DelegateString()

        // lazy 위임은 val 키워드로 선언되어야만 가능함
        // 네트워크에서 받은 텍스트는 시간이 걸리므로 실제로 사용할 때 초기화
        val httpText by lazy {
            println("lazy init start")
            InputStreamReader(URL("http://www.naver.com").openConnection()).readText()
        }

        // name 프로퍼티 값이 변결될 때마다 자동으로 observale의 코드가 실행
        var name: String by Delegates.observale("") {
            property, oldValue, newValue ->
            println("기존값: ${oldValue}, 새로적용될값: ${newValue}")
        }
    }
    ```
3. 프로퍼티를 Map 객체에 위임
- Map객체는 Key, Value로 이루어져 있음  
특정 Key에 해당하는 Value를 저장하는 자료구조

```kotlin
// 예제

// Animal 클래스는 map 객체를 생성자에서 받는다
class Animal(val map:MutableMap<String, Any?>) {
    // 프로퍼티를 map 객체로 위임한다. map 객체에서 값을 읽고,
    // 값을 변경하면 map 객체에서 값이 변경된다.
    var name: String by map
    var age: Int by map
}

@Test
fun testAnimalByMap() {
    // Animal 객체를 생성할 때 맵 객체를 넘김
    val animal = Animal(mutableMapOf(
        "name" to "cat",
        "age" to 20)
    )

    // name 속성이 map 객체에 정상적으로 위임되었는지 확인
    Assert.assertEquals("cat", animal.name)
    // age 속성이 map 객체에 정상적으로 위임되었는지 확인
    Assert.assertEquals(20, animal.age)

    // 프로퍼티의 값을 변경
    animal.age = 21
    animal.name = "dog"

    // map의 값들이 바꼈는지 확인
    Assert.assertEquals("dog", animal.map["name"])
    Assert.assertEquals(21, animal.map["age"])
}

// Animal객체를 생성할 때 MutableMap을 생성자로 전달
// 단지 이 작업만으로도 Animal 클래스의 name, age 프로퍼티가 초기화
// name, age의 속성은 Getter, Setter가 Map으로 위임
// 그렇기 때문에 이후 name, age 프로퍼티는 값을 읽을 때에도 전달받은 Map객체의 값을 읽게 되고,
// 값을 변경하면 Map객체의 Key에 해당하는 Value가 바뀌게 됨
```

## 내부 클래스와 중첩 클래스
- ```java
  // Java
  // 예제
  
  public class SampleClass {
      int outerField1 = 0;
      
      // 클래스 내부에 선언된 클래스를 내부 클래스(Inner Class)라고 함
      // 내부 클래스는 외부로 선언된 SampleClass 객체가 생성되어야 존재 O
      class InnerClass {
          // 내부 클래스에서는 외부 클래스의 필드에 접근 가능
          int myField = outerField;
      }
  
      // 클래스 내부에 선언되어 있지만 static이 붙으면 중첩 클래스가 됨
      // 중첩 클래스는 외부에 있는 SampleClass객체가 없어도 존재할 수 있음
      public static class NestedClass {
          // 중첩 클래스는 외부 클래스 필드에 접근이 불가능
          // int myField = outerField1;
      }
  }
  
  // 내부 클래스가 존재한다는 것은 반드시 외부에 있는 SampleClass 객체도 존재한다는   의미
  // 그렇기 때문에 외부에 있는 SampleClass의 필드에 접근할 수 있음
  
  // 반면 중첩 클래스는 외부에 있는 SampleClass의 존재와 관계없이 독립적으로 존재할   수 있음
  // 그렇기 때문에 외부에 있는 SampleClass의 필드에 접근할 수 없음
  // 중첩 클래스가 있다고 해서 SampleClass객체가 반드시 존재하는 것은 아니기 때문
  ```
- Java와 코틀린에 있어 중첩 클래스와 내부 클래스의 기본 설정이 다름
  ```kotlin
  // 예제
  class Sample {
      val field1 = 0
  
      // 코틀린은 내부에 클래스를 선언하면 중첩 클래스가 됨
      class NestedClass {
          // 중첩 클래스에서는 외부 클래스 속성에 접근 불가
          // val myField = field1
      }
  
      // 코틀린에서 내부 클래스를 선언하려면 inner 키워드 사용
      inner class InnerClass {
          // 내부 클래스에서는 외부 클래스의 속성에 접근 가능
          val myField = field1
      }
  }
  
  // 코틀린에서도 중첩 클래스와 내부 클래스의 차이점은 같음
  // 내부 클래스는 외부 클래스의 속성에 접근이 가능하며, 중첩 클래스는 접근할 수 없음
  // 클래스 내부에 클래스를 선언하는 경우 중첩 클래스가 됨
  ```
- 접근제한자를 중첩클스와 내부 클래스에 붙이다면
  - 접근제한자를 활용해 중첩 클래스를 쓰게 되면 외부에 노출하지 않아도 되는 코드를 클래스 단위로 묶어서 관리하는데 도움이 됨
  ``` kotlin
  // 예제

  class OuterClass{
  // 중첩클래스
    private class NestedClass{
      val a = 1
    }
    fun method1() = NestedClass().a
    // 에러 'public' function exposes
    // its 'private' return type NestedClass
    fun method2() = NestedClass()
  }
  fun main(args: Array<String>) {
      // 에러 : Cannot access 'NestedClass': it is private in 'OuterClass'
      // 더 이상 OuterClass.NestedClass형태로 접근할 수 없고 인스턴스 조차 공유 X
      println(OuterClass.NestedClass)
      // 결과 : 1
      println(OuterClass().method1())
  }
  ```
  - 내부 클래스는 private 접근제한자를 쓰는게 메모리 관리 측면에서 더욱 안전할 수 있음
  - ```kotlin
    // 예제

    class OuterClass{
    // 내부클래스
    private inner class InnerClass{
      val a = 1
    }
    fun method1() = InnerClass().a
    // 에러 : 'public' function exposes
    // its 'private' return type NestedClass
    // 내부 클래스도 private 접근제한자를 쓰면 중첩클래스와 동일하게 내부클래스의 인스턴스를 외부에 공개되지 않음
    fun method2() = InnerClass()
  }
  ```

## Collectioin의 함수형 API
- 컬랙션 APi
    - filter = 컬렉션에서 조건에 맞는 항목과 추출해 새로운 컬렉션을 반환
    - map = 컬렉션에 항목을 변환하여 새로운 컬렉션을 만들고 반환
    - flatmap = 컬렉션의 포함된 항목들을 평형하게 펼친 뒤 변환하여 새로운 컬렉션 반환
    - find = 함수의 조건을 만족하는 항목 한 개를 반환
    - group by = 컬렉션을 여러 그룹으로 이뤄진 맵으로 변경
```kotlin
@Test
fun testCollectionApi() {
    // 컬렉션을 만듬
    val list = listOf(1, "2", 3, 4, 5.7, 1, 2)

    // filter : 컬렉션에서 특정 조건이 맞는 항목만 추출하여 컬렉션 제작 -> Int 타입만 추출
    println(list.filter{item -> item is Int})

    // 람다 표현식에서 파라미터가 하나인 경우 생략이 가능
    // 파라미터는 it 키워드로 접근 가능
    println(list.filter {it is Int})

    // map : 컬렉션에서 아이템을 변환하여 새로운 컬렉션을 만듬. 
    // 아래 코드는 String의 컬렉션이 만들어짐
    println(list.map{ "value: ${it}" })

    // filter에서 반환된 컬렉션을 map으로 변환
    println(list.filter { it is Int}.map {"value: ${it}" })

    // 아이템을 찾음
    println(list.find { it is Double })

    // 컬렉션을 그룹화하여 Map<String, List<T>> 형태로 만듬.
    // 아래 코드는 각 아이템의 클래스 별로 그룹화 됨
    val map = list.groupBy{ it.javaClass }
    println(map)

    // 컬렉션 안에 컬렉션이 있는 새로운 리스트를 만듬
    val list2 = listOf(listOf(1, 2), listOf(3, 4))
    println(list2)

    // map으로 항목을 변환
    println(list2.map{ "value: ${it}" })

    // flatmap으로 리스트를 평평하게 만들고 변환
    println(list2.flatMap{ it.toList() })
}
```

## 확장 함수
- 이미 정의된 클래스를 전혀 수정하지 않고도 클래스에 포함된 함수처럼 사용할 수 있음
```kotlin
// 예제

// String 클래스에 lastString 확장함수를 추가로 정의함
fun String.lastString(): String {
    return this.get(this.length - 1).toString()
}

@Test
fun testExtensions() {
    val str = "Hello, Extensions"
    // lastString() 함수를 원래 String 클래스의 메소드처럼 사용 가능
    Assert.assertEquals("s", str.lastString())
}

// 위 코드를 보면 마치 원래 String 클래스 내부에 선언된 메소드처럼 사용
// 이렇게 실제로 클래스의 메소드는 아니지만, 클래스 외부에서 선언하고
// 마치 클래스의 메소드처럼 사용하는 것을 확장 함수라고 함
// Java에서도 사용 가능
```

## 널 안정성(Null Safety)
- null  = 무엇인가 `없다`라는 의미
- NullPointerException = NPE 예외 = 객체의 참조가 널이어서 발생하는 예외 
```kotlin
// 예제

// 코틀린 타입은 기본적으로 널(NULL)을 허용하지 않음
fun strLenNonNull(str: String): Int {
    // 파라미터로 받은 str은 널이 될 수 없으므로 안전
    return str.length
}

// 만일 널(NULL) 가능성이 있다면 타입에 ?를 붙여야 함
fun strLenNullable(str: String): Int {
    // 널 가능성이 있는 str 메소드에 접근하면 에러가 발생
    // return str.length

    // if로 널체크
    if(str != null) {
        // 널체크 이후 str은 String? 타입에서 String 타입으로 스마트 캐스팅됨
        return str.length
    } else {
        return 0
    }
}

// 문자열 끝 Char를 반환
fun strLastCharNullable(str: String?): Char? {
    // ?. 연산자는 str이 NULL이면 null이 반환됨
    // (null이면 null을 반환, 아닐 때는 그대로 진행)
    return str?.get(str.length - 1)
}

// 문자열 끝 Char를 반환
fun strLastCharNullable(str: String?): Char? {
    // ?. 연산자를 사용하여 str이 널이면 "".single()이 반환됨
    // (null이면 : 뒤 코드를 반환, 아닐 때는 그대로 진행)
    return str?.get(str.length - 1) ?: "".single()
}

// let 함수를 이용한 예제
fun strPrintLen(str: String?) {
    // let 함수는 수신객체인 str이 널이면 실행되지 않음
    // '수신 객체가 널이 아닌 경우'에만 람다 함수 실행
    str?.let { print(strLenNonNull(it)) }
}

// as 연산자는 타입 캐스팅을 시도한 대상의 값을 지정한 타입으로 변환할 수 없는 경우,
// Java에서와 같이 ClassCastException이 발생
// 물론 클래스 캐스트를 할 때 is 연산자로 캐스팅이 가능한지 확인할 수 있지만,
// as? 연산자를 사용하여 편리하고 안전하게 캐스팅 가능

class Truck(val id: Int, val name: String) {
    // equals를 오버라이드함, id가 같으면 같은 객체로 취급
    override fun equals(other: Any?): Boolean {
        // as? 연산자를 사용하면 타입이 같은 경우 캐스팅이 정상적으로 되고
        // 캐스팅이 실패하면 null이 반환
        // null이 반환된 경우 엘비스 연산자의 디펄트 식이 실행되어 false가 리턴
        val otherTruck = other as? Truck ?: return false

        // otherTruck은 스마트 캐스팅되어 널을 신경쓸 필요가 없음
        return otherTruck.id == id
    }
}
// 타입 캐스팅을 시도할 때 타입이 맞는 경우엔 스마트 캐스팅이 되고,
// 만일 실패하면 널이 반환되므로 엘비스 연산자가 실행되어 함수에서 false를 반환

// !!를 사용하여 null이 아니라고 할 수 있음
fun ignoreNull(s: String?) {
    val stringNotNull : String = s!!
    // stringNotNull은 null이 아닌 값으로 인식됨
    println(stringNotNull.length)
}
```
<출처>안드로이드 Kotlin 앱프로그래밍 가이드   
<출처>https://0391kjy.tistory.com/53
<br/>
<br/>

## Object
object로 `싱글턴 클래스`를 정의할 수 있음   
object는 다음과 같은 경우에 사용됨
- 싱글턴 클래스로 만들 때
- 익명 클래스 객체를 생성할 때
```kotlin
// 예제

// object로 싱글턴 클래스를 정의할 수 있음
object CarFactory {
    val cars = mutableListOf<Car>()

    fun makeCar(horsepowers: Int) : Car {
        val car = Car(horsepowers)
        cars.add(car)
        return car
    }
}

class Car(power: Int) {}

// 아래 코드처럼 메소드에 접근하여 Car객체를 생성할 수 있음
// 또한 변수에 접근할 수 있음
// CarFactory 객체는 싱글톤으로 구현이 되었기 때문에 여러번 호출해도 CarFactory 객체는 한 번만 생성

val car = CarFactory.makeCar(150)
println(CarFactory.cars.size)

```
<출처>https://codechacha.com/ko/kotlin-object-vs-class/
<br/>
<br/>

## Companion Object
- companion object는 java에 static으로 동작하는 것처럼 보일 뿐, static이 아님
  ```kotlin
  // 예제

  class MyClass2{
      companion object{
          val prop = "나는 Companion object의 속성이다."
          fun method() = "나는 Companion object의 메소드다."
      }
  }
  fun main(args: Array<String>) {
      //사실은 MyClass2.맴버는 MyClass2.Companion.맴버의 축약표현이다.
      println(MyClass2.Companion.prop)
      println(MyClass2.Companion.method())
  }
  ```
  companion object{}는 MyClass2 클래스가 메모리에 적재되면서 함께 생성되어 `동반(companion)되는 객체`이고   
  이 동반 객체는 클래스명.Companion으로 접근할 수 있음(하지만 축약해서 사용)
- companion object는 객체
  ```kotlin
  // 예제

  class MyClass2{
      companion object{
          val prop = "나는 Companion object의 속성이다."
          fun method() = "나는 Companion object의 메소드다."
      }
  }
  fun main(args: Array<String>) {
      println(MyClass2.Companion.prop)
      println(MyClass2.Companion.method())
      // companion object는 객체이므로 변수에 할당 가능
      val comp1 = MyClass2.Companion 
      // 그리고 할당한 변수에서 MyClass2에 정의된 companion obbject의 멤버에 접근 가능(java의 static에서는 불가능)
      println(comp1.prop)
      println(comp1.method())

      // 클래스 내 정의된 companion object는 클래스 이름만으로도 참조 접근이 가능
      val comp2 = MyClass2
      println(comp2.prop)
      println(comp2.method())
  }
  ```
- companion object에 이름을 설정 가능
  ```kotlin
  // 예제

  class MyClass3{
      companion object MyCompanion{  // -- (1)
          val prop = "나는 Companion object의 속성이다."
          fun method() = "나는 Companion object의 메소드다."
      }
  }
  fun main(args: Array<String>) {
      // 사용 가능
      println(MyClass3.MyCompanion.prop)
      println(MyClass3.MyCompanion.method())
      
      // 사용 가능
      val comp1 = MyClass3.MyCompanion
      println(comp1.prop)
      println(comp1.method())

      // 사용 가능
      val comp2 = MyClass3
      println(comp2.prop)
      println(comp2.method())
      
      // 사용 불가능(이름을 설정했기 때문)
      val comp3 = MyClass3.Companion
      println(comp3.prop)
      println(comp3.method())
  }
  ```
- 인터페이스 내에 companion object를 정의 가능
  ```kotlin
  // 예제

  interface MyInterface{
      companion object{
          val prop = "나는 인터페이스 내의 Companion object의 속성이다."
          fun method() = "나는 인터페이스 내의 Companion object의 메소드다."
      }
  }
  fun main(args: Array<String>) {
      println(MyInterface.prop)
      println(MyInterface.method())
      val comp1 = MyInterface.Companion
      println(comp1.prop)
      println(comp1.method())
      val comp2 = MyInterface
      println(comp2.prop)
      println(comp2.method())
  }
  ```
- 상속 관계에서 companion object 멤버는 같은 이름일 경우 가려짐(shadowing)
  ```kotlin
  // 예제

  open class Parent{
      companion object{
          val parentProp = "나는 부모값"
      }
      fun method0() = parentProp
  }
  class Child:Parent(){
      companion object{
          val childProp = "나는 자식값"
      }
      fun method1() = childProp
      fun method2() = parentProp
  }
  fun main(args: Array<String>) {
      val child = Child()
      println(child.method0()) //나는 부모값
      println(child.method1()) //나는 자식값
      println(child.method2()) //나는 부모값
  }
  // 부모/자식의 companion object의 멤버가 다른 이름이라면 자식이 부모의 companion object 멤버를 직접 참조할 수 있음
  ```
  이름이 같아지면 자식 클래스의 companion object가 부모의 companion object에 가려짐
- 클래스 내 companion object는 딱 하나만 사용 가능
- 중첩 클래스에서는 companion 클래스를 정의할 수 없음. 하지만 내부 클래스에서는 정의 가능
<출처>https://www.bsidesoft.com/8187, https://www.bsidesoft.com/8218

## Coroutine
코루틴이 시작된 스레드를 중단하지 않으면서 `비동기적`으로 실행되는 코드(async와 await같은 느낌?)
- 코루틴 스코프
    - 모든 코루틴은 스코프 내에서 실행되어야 하는데 이를 통해서 액티비티 또는 프르개믄터의 생명주기에 따라 소멸 될 때   
    관련 코루틴을 한번에 취소할 수 있는데 이는 곧 메모리 누수를 방지
    - 스코프는 이미 내장된 범위를 사용할 수 있음
    - 스코프 종류
        - 글로벌 스코프 : 앱의 생명주기와 함께 동작하기 때문에 실행 도중에 별도 생명 주기 관리가 필요없음.   
        시작 ~ 종료까지 긴기간 실행되는 코루틴의 경우에 적합
        - 코루틴 스코프 : 버튼을 눌러 다운로드 하거나 서버에서 이미지를 열 때 등,   
        필요할 때만 열고 완료되면 닫아주는 코루틴스코프를 사용할 수 있음   
        글로벌 스코프와 다릴 디스패쳐를 지정할 수 있는데 이는 코루틴이 실행될 스레드를 지정하는 것
        - ViewModelScope : Jetpack 아키텍쳐의 뷰모델 컴포넌트 사용시 ViewModel 인스턴스에서 사용하기 위해 제공되는 스코프   
        해당 스코프로 실행되는 코루틴 뷰모델 인스턴스가 소멸될 때 자동으로 취소

        <br/>
- 코루틴 디스패쳐
    - Dispatchers.Default : 안드로이드 기본 스레드풀 사용. CPU를 많이 쓰는 작업에 최적화(데이터 정렬, 복잡한 연산 등)
    - Dispatchers.IO : 이미지 다운로드, 파일 입출력 등 입출력에 최적화 되어있는 디스패쳐(네트워크, 디스크, DB 작업에 적합)
    - Dispatchers.Main : 안드로이드 기본 스레드에서 코루틴 실행. UI와 상호작용에 최적화
    - Dispatchers.Unconfined : 호출한 컨텍스트를 기본으로 사용하는데 중단 후 다시 실행될 때 컨텍스트가 바뀌면 바뀐 컨텍스트를 따라가는 특이한 디스패쳐
- 기본
    - runBlocking { 코드 } : 비동기가 아닌 동기로 처리
    - launch { 코드 } : 독립적으로 계속 작동하는 나머지 코드와 동시에 새 코루틴을 시작, 반환값이 없는 Job 객체
    - delay(timeMillis: Long) : timeMillis만큼 일시 중단
    - suspend : 함수(fun 키워드) 앞에 붙일 시 launch 안에서 사용가능한 함수로 만듬
    - job.cancelAndJoin() : 작업을 취소하고 완료될 때까지 기다림
    - try { 실행코드 } finally { 마지막 코드 } : 실행코드가 끝나면 마지막 코드를 실행(중간에 실행코드가 끝나도 마지막 코드 실행)
    - async { 코드 } : launch와 기능이 같음, 하지만 반환값이 있는 Deffered 객체(마지막 값 return)

    <br/>

    - coroutinScope : 고유한 범위를 선언할 수 있음. 코루틴 범위를 만들고 실해오딘 모든 자식이 완료될 때까지 완료되지 않음
        - runBlocking과 coroutineScope의 차이점 : runBlocking메소드는 대기를 위해 현재 스레드를 차단하는 반면 coroutineScope는 일시 중단되어 다른 용도를 위해 기본 스레드를 해제   
        따라서 runBlocking은 일반 함수, coroutineScope는 일시 중단 함수
        - ``` kotlin
          // 예제
          fun main() = runBlocking { doWorld() }

          suspend fun doWorld() = coroutineScope { // this : CoroutineScope
              launch {
                  delay(1000L)
                  println("World!)
              }
              println("Hello)
          }
          // 출력 결과
          // Hello
          // World!
          ```
        - 동시에 여러 개의 코루틴을 사용할 수 있음
          ``` kotlin 
          fun main() = runBlocking {
              // runBlocking 안에 있으므로 doWorld가 끝난 후 "Done"을 출력
              doWorld()
              println("Done")
          }

          suspend fun doWorld() = coroutineScope { // this : CoroutineScope
              launch {
                  delay(2000L)
                  println("World2")
              }
              launch {
                  delay(1000L)
                  println("World1")
              }
              println("Hello")
          }
          // 출력 결과
          // Hello
          // World1
          // World2
          // Done
          ```
    - 명시적 작업
      ``` kotlin
      val job = launch { // 새 코루틴을 시작하고 해당 작업에 대한 참조를 유지
          delay(1000L)
          println("World!")
      }
      println("Hello")
      job.join() // 자식 코루틴이 완료될 때까지 기다림
      println("Done")
      
      // 출력 결과
      // Hello
      // World!
      // Done
      ```
- 취소할 수 없게 실행
  ``` kotlin
  val job = launch {
      try {
          repeat(1000) { i ->
              println("job: I'm sleeping $i ...")
              delay(500L)
          }
      } finally {
          withContext(NonCancellable) {
              println("job: I'm running finally")
              delay(1000L)
              println("job: And I've just delayed for 1 sec because I'm non-cancellable")
          }
      }
  }
  delay(1300L) // 약간 지연
  println("main: I'm tired of waiting!")
  job.cancelAndJoin() // 작업을 취소하고 완료될 때까지 기다림
  println("main: Now I can quit.")

  // 출력 결과
  // job: I'm sleeping 0 ...
  // job: I'm sleeping 1 ...
  // job: I'm sleeping 2 ...
  // main: I'm tired of waiting!
  // job: I'm running finally
  // job: And I've just delayed for 1 sec because I'm non-cancellable
  // main: Now I can quit.
  ```
- 시간 제한
    - 예외 발생
      ``` kotlin
      withTimeout (1300L) {
          repeat(1000) { i ->
              println("I'm sleeping $i ...")
              delay(500L)
          }
      }
      // 출력 결과
      // I'm sleeping 0 ...
      // I'm sleeping 1 ...
      // I'm sleeping 2 ...
      // Exception in thread "main" kotlinx.coroutines.TimeoutCancellationException: Timed out waiting for 1300 ms
      ```
    - 예외 없애기
      ``` kotlin
      //
      val result = withTimeoutOrNull(1300L) {
          repeat(1000) { i -> 
              println("I'm sleeping $i ...")
              delay(500L)
          }
          "Done" // 이 결과를 생성하기 전에 취소됨
      }
      println("Result is $result")

      // 출력 결과
      // I'm sleeping 0 ...
      // I'm sleeping 1 ...
      // I'm sleeping 2 ...
      // Result is null
      ```
- 비동기 지연
    - async 매개 변수에 CoroutineStart.LAZY로 설정해 async를 지연 가능
      ``` kotlin
      suspend fun doSomethingUsefulOne(): Int {
          delay(1000L) // 대충 엄청난 작업들
          return 13
      }
  
      suspend fun doSomethingUsefulTwo(): Int {
          delay(1000L) // 대충 엄청난 작업들
          return 29
      }

      val time = measureTimeMillis {
          val one = async(start = CoroutineStart.LAZY) { doSomethingUsefulOne() }
          val two = async(start = CoroutineStart.LAZY) { doSomethingUsefulTwo() }
          // 일부 계산
          one.start() // 첫 번째 시작
          two.start() // 두 번째 시작
          println("The answer is ${one.await() + two.await()}")
      }
      println("Completed in $time ms")

      // 출력 결과
      // The answer is 42
      // Completed in 1013 ms
      ```
- 비동기식 함수
    - ``` kotlin
      suspend fun doSomethingUsefulOne(): Int {
          delay(1000L) // 대충 엄청난 작업들
          return 13
      }

      suspend fun doSomethingUsefulTwo(): Int {
          delay(1000L) // 대충 엄청난 작업들
          return 29
      }

      // GlobalScope는 섬세한 API여서 명시적으로 선택해야 함
      @OptIn(DelicateCoroutinesApi::class)
      fun somethingUsefulOneAsync() = GlobalScope.async {
          doSomethingUsefulOne()
      }

      @OptIn(DelicateCoroutinesApi::class)
      fun somethingUsefulTwoAsync() = GlobalScope.async {
          doSomethingUsefulTwo()
      }

      fun main() {
          val time = measureTimeMillis {
              // 코루틴 외부에서 비동기 작업을 실행 가능
              val one = somethingUsefulOneAsync()
              val two = somethingUsefulTwoAsync()

              // 그러나 결과를 기다리는 것은 일시 중단 또는 차단을 포함해야 함
              // 여기서 runBlocking {}을 사용하여 결과를 기다리는 동안 메인 스레드를 차단
              runBlocking {
                  println("The answer is ${one.await() + two.await()}")
              }
          }
          println("Completed in $time ms")
      }
      // 출력 결과
      // The answer is 42
      // Completed in 1132 ms
      // 시작한 작업이 오류가 생겨서 중단되었음에도 불구하고 백그라운드에서 실행되기 때문에 코루틴과 함께 이 스타일을 사용하는 것은 강력히 권장하지 않음
      ```
- 비동기를 사용한 구조적 동시성
    - ``` kotlin
      suspend fun doSomethingUsefulOne(): Int {
          delay(1000L) // 대충 엄청난 작업들
          return 13
      }

      suspend fun doSomethingUsefulTwo(): Int {
          delay(1000L) // 대충 엄청난 작업들
          return 29
      }
    
      // 이렇게 하면 함수 코드 내에서 문제가 발생하여 예외가 발생하면 해당 범위에서 시작된 모든 코루틴 취소
      // 비동기식 대신 이 방식 선호
      suspend fun concurrentSum(): Int = coroutineScope {
          val one = async { doSomethingUsefulOne() }
          val two = async { doSomethingUsefulTwo() }
          one.await() + two.await()
      }

      val time = measureTimeMillis {
          println("The answer is ${concurrentSum()}")
      }
      println("Completed in $time ms")
      ```
    - 취소는 항상 코루틴 계층 구조를 통해 전파
      ``` kotlin
      fun main = runBlocking<Unit> {
          try {
              failedConcurrentSum()
          } catch(e: ArithmeticException) {
              println("Computation failed with ArithmeticException")
          }
      }

      suspend fun failedConcurrentSum(): Int = coroutineScope {
          val one = async<Int> {
              try {
                  delay(Long.MAX_VALUE)
                  42
              } finally {
                  println("First child was cancelled")
              }
          }
          val two = async<Int> {
              println("Second child throws an exception")
              throw ArithmeticException()
          }
          one.await() + two.await()
      }
      // 출력 결과
      // Second child throws an exception
      // First child was cancelled
      // Computation failed with ArithmeticException
      ```
      자료구조
      https://librewiki.net/wiki/%EC%8B%9C%EB%A6%AC%EC%A6%88:%EC%88%98%ED%95%99%EC%9D%B8%EB%93%AF_%EA%B3%BC%ED%95%99%EC%95%84%EB%8B%8C_%EA%B3%B5%ED%95%99%EA%B0%99%EC%9D%80_%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B3%BC%ED%95%99/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98_%EA%B8%B0%EC%B4%88

      https://visualgo.net/ko