# Swift Basic 2 - 9 

## 목차

* 서론

* 클로저를 구성하는 것들

* 후행 클로저

* 클로저에 대해 쓰면서...

### 서론

Python, JavaScript에서 다뤄온 클로저(closure)와 swift의 클로저는 다르다.


```python
# 람다(익명함수)

add2 = lambda x : x + 2 

# 클로저(closure)

def makeAdderOf(n : int):
    def adder(x):
        return x + n
    return adder

add10 = makeAdderOf(10)
print(add10(90)) # 100
``` 

파이썬에서의 람다와 클로저 (위)

```javascript
# 람다 (화살표 함수)

(x => x +2)(3) // 5

# 클로저(closure)

function makeAdderOf( num ){
    return function(x){
        return x + num;
    };
}

add10 = makeAdderOf(10);
console.log(add10(90)) // 100      
```

자바스크립트의 람다(화살표 함수)와 클로저 (위)

```swift

let add10: (Int) -> Int = { (a: Int) in a + 10 }

print(add10(90)) // 100
```

스위프트에서 말하는 클로저 (위)

앞서 설명하기 전에 스위프트에서 말하는 **클로저**는 파이썬과 자바스크립트의 람다와 유사하다.

**Swift의 클로저 == 람다 함수 (익명 함수)** 헷갈리지 말자!


### 클로저를 구성하는 것들

앞서서 클로저 또한 함수이므로 함수장에서 언급된 모든 특징을 적용할 수 있다.

```swift
let add10 : (Int) -> Int = { ( a : Int) in 
    return a + 10 
}   
```

가장 기본적으로 클로저의 구성 형태는 다음과 같다. 

```
let <변수명> : (파라미터 자료형1, 자료형2, ... ) -> 반환되는 자료형 {
    (nickName1 : 자료형1, nickName2 : 자료형2, ...) in 
    함수 구현 내부 ... (일반 함수와 같음)
}
```

클로저도 함수이므로 함수를 쓸 때 이용한 단축인자($0, $1, .. )를 이용할 수 있다.(아래)

```swift
let add10 : (Int) -> Int = {$0 + 10}
```

클로저의 구현할 식이 짧으면 위와 같이 파라미터 이름과 타입을 지정할 필요가 없으며, 'in'도 안써줘도 된다.

맨 마지막의 표현식은 함수(function)에서도 다뤘듯이, 암시적으로 return하는 값이라고 swift가 이해한다.

```swift
typealias IntInt = (Int) -> (Int)

let add : IntInt = { $0 + $1 }
```

typealias 를 이용해서 위와 같이 더 줄일 수도 있다.

### 후행 클로저

후행 클로저라는 이름이 따로 있다고 기능이나 특징이 다른게 아니다.

후행 클로저는 마지막의 파리미터가 클로저인 경우, 파라미터가 길어질 수 있다.

그래서 파라미터를 감싸는 소괄호 (,  )가 여러 줄을 걸쳐 감싸는게 못마땅한 Swift 개발자가 만든것으로 추정된다.

소괄호가 여러줄에 걸쳐 감싸는 구조는 Java에서 클로저(람다 함수)를 쓰는 경우 많이 보인다(특히 자바 쓰레딩). 

```swift
// 파라미터를 받아 파라미터로 넣은 클로저로 무언가를 하는 함수

func calculate(_ a : Int,_  b : Int, adder : (Int, Int) -> Int) -> Int {
    return adder(a, b)
}

/*
파라미터 :
1. a : Int = 더할 숫자 1
2. b : Int = 더할 숫자 2
3. adder : (Int, Int) -> Int = 내가 넣을 adder 클로저
*/
```

클로저를 파라미터로 넣어 함수에서 쓰이도록 한다. 

```swift
let sum : Int = calculate(10, 20) { 
    $0 + $1 + 9 
}
print(sum) // 39

// Same as...
let sum : Int = calculate(10, 20, adder: { 
    $0 + $1 + 9
})
print(sum) // 39
```

만약 클로저를 받아들이는 파라미터가 2개 이상 있다면 다음과 같이 된다.

```
func calculate(_ a : Int,_  b : Int, adder : (Int, Int) -> Int, adder2 : (Int, Int) -> Int ) -> Int {
    return adder(a, b)
}

let sum : Int = calculate(10, 20, adder: {$0 + $1 + 8}) { $0 + $1 + 9 }
print(sum) // 39
```

### 클로저에 대해 쓰면서...

언어마다 화살표 함수, 람다 함수, 클로저, 등 다양한 이름으로 불리고 있는 람다는 처음에 이해하기 어려운 개념일 수 있다.

자연스럽게 익히는 개념중 하나라서, 처음 접해본 초보자가 정확히 이론적으로 뭔지 배우기 모호한 면이 있다고 생각한다.

람다와 관련된 블로그 글이 많지만, 

각자 사용하는 프로그래밍 언어에 따라서 부르는 이름과 문법이 달라서 혼동을 일으키기 쉬운 개념이다.

그래서 람다와 클로저의 정의를 우선 알아본 다음에 접하는 것도 나쁘지 않다고 생각한다.

클로저를 공부하면서 언어의 메모리 관리 구조에 대한 공부의 호기심을 이어 가졌으면 하는 바램이 있다.
