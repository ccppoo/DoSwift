# Swift Basic - 1

**불변/가변 자료형**과 **기본 자료형 타입**에 대해 간단히 알아본다.

## 상수(불변) 자료형, 가변 자료형

### 1. 상수 자료형

다른 언어에서 한번 선언 후 읽기만 가능한 자료형의 경우 let, val, const 키워드를 쓰는 것과 같다.

```swift
let nickName = "ccppoo"
```

프로그래밍을 하다보면 프로그램 실행 시점 이전(컴파일 시점)에 상수값을 모르는 경우 (예:이름)

일단 필요한 데이터의 이름('nickName')과 자료형('String')을 선언만 해도 된다.

\# lazy initialization

```swift
let nickName : String;

nickName = "ccppoo";

nickName = "nnppoo" // Error
```

### 2. 가변 자료형 (변수)

다른 언어에서 한번 선언 후 읽고 수정이 가능한 자료형의 경우 var과 같다.

```swift
var age = 22;
```

## 자료형 타입

Swift는 짜증날 정도로 자료형 타입이 많은 편이다.

자료형 타입을 보다보면 C/C++ 언어를 보는 기분이 들기도 한다.

자료형은 크게 기본적으로 Swift에서 기본적으로 제공하는 **원시 타입(Primitive Type)**과 사람들이 만들어 새로 정의하는 자료형(Class)이 있다.

> 클래스를 자료형 타입이라고 말하는 이유는 프로그램 스크립트의 문맥상 클래스 또한 하나의 자료형으로 취급하며,
> 클래스는 다양하고 여러가지의 기본 자료형을 가진 하나의 '타입'이기 때문이다.

### 0-1. 값(변수) 자료형과 함께 선언하기 - 중요!

Swift와 같은 (대부분의) 고급 언어는 자료형 추론을 지원한다.

추론은 단어 그대로 Swift 컴파일러가 선언된 데이터가 어떤 자료형인지 추론을 하는 것이다.

```swift
var myName = "ccppoo" // 컴파일러 : "이건 String 자료형이군"
```

위의 코드는 아래와 같이 컴파일러가 해석한다

```swift
var myName : String = "ccppoo"
```

하지만, 컴파일러가 **추측**을 하는 것이기 때문에 내가 의도했던 자료형과 달리 다른 자료형으로 추론할 수 있어
</br> 예상치 못한 파장이 일어날 수 있다... 그 파장이 무서움으로 예시는 들지 않겠다.

```swift
\# 사용자의 의도 -> '캐릭터 HP는 0아래로 내려갈 일도 없지'

var playerHP = 300;

\# 컴파일러의 추측 -> '정수네 그럼 그냥 Int로 써야지'

var playerHP : Int = 300; // 나중에 HP가 음수로 되는 경우 문제를 파악하기 어렵다
```

### 0-2. 서로 다른 자료형에 값을 대입할 수 없다.

자료형이 많은 만큼 Swift는 자료형을 자동으로 캐스팅(Casting)해주지 않는다.

처음에는 이런 점이 Python이나 JavaScript에 비해 불편하다고 느낄 수 있지만,

프로그래머가 데이터를 다룰 때 상황을 정확하게 파악하도록 하게끔 유도할 수 있어, '안전한' 프로그래밍이 가능해진다.

```swift
var myString : String = "ccppoo";
var myChar : Character = "A";

myString = myChar // Error
```

### 1. 문자와 관련된 자료형

대표적으로 많이 쓰는 문자(열) 자료형은 String(문자열)과 Character(문자)이다.

나중에 코딩을 하다보면 문자열 코덱(Codec)과 JSON 작업을 하면 엄청 스트레스를 받는 부분이다.

String은 Character 자료형의 super set과 같다.

String은 하나 이상의 문자, Character는 이모지를 포함한 하나의 문자를 담을 수 있는 자료형이다.

```swift
let myName : String = "ccppoo";
let myScore : Character = "A";
let yourScore : Character = "A+"; // Error
```

문자와 관련된 자료형은 Apple의 산물인 object-c에서 내려온 자료형과 더불어 엄청나게 많기 떄문에 파도파도 넘쳐난다.

문자열은 더하기 연산자 '+'를 이용해 합성할 수 있다. 

```swift
let sayHi : String = "Hi " + myName; // "Hi ccppoo"
```

이외에 문자열과 관련된 메서드는 "\[String 타입의 변수 \].\[메서드 이름\](\[문자열\])"와 같이 사용하면 된다

```swift
print(sayHi.contains("c"))
```

### 2. 숫자와 관련된 자료형

대표적으로 많이 쓰는 숫자 자료형은 Int(정수), Float(실수), Double(더 큰 실수)이다.

숫자와 관련된 자료형 또한 많으므로 고통받을 수 있다.

```swift
let myScore : Int = 90;
let yourScore : Double = 90.1;
let hisScore : Int = 90.2; // Error
```

### 3. 부울린 값 참/거짓, Bool(Boolean)

True, False 값 두가지가 존재한다.