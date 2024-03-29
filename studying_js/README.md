# Studying JS

<details>
<summary>var / let / const & Hoisting</summary>

### var, let, const
- 자바스크립트에서 변수를 선언할 때 var, let, const를 사용한다.

#### 변수 선언 방식
- var : 중복 선언과 재할당이 가능하다.
- let(ES6) : 중복 선언은 불가하며, 재할당은 가능하다.
- const(ES6) : 중복 선언과 재할당 둘 다 불가능하다.
  - 하지만 const로 선언했어도 배열과 객체의 값을 변경하는 것은 가능

#### 유효한 참조 범위(Scope)
- var : 함수 레벨 스코프(function-level scope)
  - 함수 내에서 선언된 변수는 함수 내에서만 유효하다.(함수 내에서는 블록 내외부에 관계없이 유효)
  - 하지만 함수 외부에서는 참조 불가
  ```javascript
    function func() {
        if(true) {
            var a = 'a';
            console.log(a); // 'a'
        }
        console.log(a); // 'a'
    }
    func();
    console.log(a); // error
  ```
- let / const : 블록 레벨 스코프(block-level scope)
  - 함수, if문, for문, while문, try / catch문 등의 모든 코드 블록 내부에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다.
  ```javascript
  function func() {
    if(true) {
        let a = 'a';
        console.log(a); // 'a'
    }
    console.log(a); // error
  }

  func()
  console.log(a) // error
  ```

### 호이스팅(Hoisting)

- 호이스트(Hoist)의 뜻은 무언가를 들어 올리거나 끌어 올리는 동작을 설명한다.
- Javascript에서 호이스팅은 코드가 실행되기 전에 변수 및 함수 선언(이름)이 로컬 범위(유효 범위)의 맨 위로 들어올려지거나 끌어올려지는 경우를 설명한다.

#### var 선언문 호이스팅
- 아리 예에서는 아직 생성하지 않은 변수에 대한 콘솔 로그를 사용하여 시작한다.
- 다음으로 greeting라는 변수를 선언하고 문자열 hello를 할당한다.
- 코드가 실행되면 undefined가 반환된다.
```javascript
console.log(greeting); // undefined
var greeting = "Hello";
```
- 이 코드가 에러를 발생시키지 않는 이유는 호이스팅 때문이다.
- Javascript 인터프리터는 변수 생성의 선언(var greeting) 단계 및 할당(="hello") 단계를 분할한다.
- 선언 부분은 코드가 실행되기 전에 현재 범위의 맨 위로 호이스팅되고 초기에 undefined 값이 할당된다. 즉, 초기화되기 전에 greeting 변수를 사용할 수 있다.
  - 변수 생성
    - 선언 단계 : undefined
    - 할당 단계 : hello 값 할당

#### 함수 선언문 호이스팅
- 함수 선언문도 함수 생성전에 호출하면 올바로 출력이 된다.
```javascript
func(); // hoisting test

function fun() {
    console.log("hoisting test");
}
```

#### let / const 선언문 호이스팅
- let 또는 const로 변수를 선언하면 실제로 변수는 여전히 호이스팅된다.
- 그러나 차이점으로 var와 비교했을 때 var는 실제 할당 값이 할당되기전까지 undefined 값이 할당된다.
- 하지만 let / const를 사용하면 변수 초기에 어떤 값도 할당되지 않는다.
```javascript
console.log(greeting);
// Uncaught ReferenceError: Cannot access 'greeting' before initialization
const greeting = "Hello";
```
![Alt text](readme_img/image.png)
- 코드가 실행되면 변수에 값이 할당하기 전에 콘솔 로그가 발생하기 때문에 위의 오류가 발생한다.
- const로 변수를 선언하는 것도 같은 방식으로 작동한다.
- 이러한 일이 발생하는 이유를 TDZ(Temporal Dead Zone)이라고 한다.
- 일시적 데드 존은 변수를 사용할 수 없는 일시적인 비활성 상태를 나타낸다.

#### let / var / const 결론
- 변수를 생성할 때 재할당이 필요없다면 const를 사용한다.
- 재할당이 필요하면 let을 사용하지만 변수의 scope를 최대한 좁게 만들어서 사용해준다.

</details>

<details>
<summary>Javascript Type</summary>

### Data Type in Javascript
- 원시 타입 : Boolean, String, Number, null, undefined, Symbol(불변성을 가지고 있다.)
- 참조 타입 : Object, Array
![Alt text](readme_img/image-1.png)
- 기본적으로 Javascript는 원시 타입에 대한 값을 저장하기 위해 Call Stack 메모리 공간을 사용하지만 참조 타입의 경우 Heap이라는 별도의 메모리 공간을 사용한다.
- 이 경우 Call Stack은 개체 및 배열 값이 아닌 Heap 메모리 참조 ID를 값으로 저장한다.
- 원시 타입 : 고정된 크기로 Call Stack 메모리에 저장. 실제 데이터가 변수에 할당.
- 참조 타입 : 데이터 크기가 정해지지 않고 Call Stack 메모리에 저장. 데이터의 값이 Heap에 저장되며 변수에 Heap 메모리의 주소값이 할당.

### Primitive Types & Object Types
#### Primitive Types
- String : 문자열
- Number : 숫자 값
- Boolean : true와 false
- Null : 하나의 값을 가진다.(null), 의도적으로 값이 없음을 나타내기 위해서 사용
- Undefined : 하나의 값을 가진다(undefined). 초기화되지 않은 변수의 기본값으로 사용
- Symbol : 변경 불가능한 유일한 값을 생성할 때 사용하며, 값 자체의 확인이 불가하여 외부로 노출되지 않는다. ES6에서 새로 생긴 타입

#### Object Types
- function : 함수
- array : 배열
- classes : 클래스
- object : 객체
![Alt text](readme_img/image-2.png)

### 자바스크립트는 동적 타입이다.
- Javascript는 느슨한 타입(loosely typed)의 동적(dynamic) 언어이다.
- Javascript의 변수는 어떤 특정 타입과 연결되지 않으며, 모든 타입의 값으로 할당(및 재할당) 가능하다.
```javascript
let foo = 42 // foo가 숫자
foo = 'bar' // foo가 이제 문자열
foo = true // foo가 이제 boolean
```
- 같은 변수가 여러개의 타입을 가질 수 있다.
- 타입을 명시하지 않아도 된다.
- 대부분의 다른 언어는 정적(static) 타입 언어이다.(자바, C#, C++)
```javascript
const name = "Han"
const age = 30
const hasJob = true
const car = null;
let anything;
const sym = Symbol();
const hobbies = ['walking', 'books']
const address = { province: '경기도', city: '성남시'}
```
- typeof array를 하면 object가 반환된다.
- 그 이유는 array가 object의 특수한 한 형태이기 때문이다.
- 그래서 배열인지 확인하기 위해서는 isArray() 메소드를 이용한다.

</details> 

<details>
<summary>Loops</summary>

### Loops
- 자바스크립트에서 루프(Loop)를 사용하면 코드 블록을 여러 번 실행할 수 있게 해준다.

### 루프의 종류
- for : 코드 블록을 여러 번 반복
- for/in : 객체의 속성을 따라 반복
- while : 지정된 조건이 true인 동안 코드 블록을 반복
- do/while : do/while 루프는 while 루프의 변형이다. 이 루프는 조건이 true인지 검사하기 전에, 코드 블록을 한 번 실행한다. 그러고 나서 조건이 true인 동안 로프를 반복한다.

</details>

<details>
<summay>Window Object</summay>

### Window Object
- window 객체는 브라우저에 의해 자동으로 생성되며 웹 브라우저의 창(window)을 나타낸다.
- 또한 window은 브라우저의 객체이지 Javascript의 객체가 아니다.
- 이 window 객체를 이용해서
  - 브라우저의 창에 대한 정보를 알 수 있고, 이 창을 제어하고 할 수도 있다.
  - 또한 var 키워드로 변수를 선언하거나 함수를 선언하면 이 window 객체의 프로퍼티가 된다.
![Alt text](readme_img/image-3.png)

</details>

<details>
<summary>DOM 이란?</summary>

### HTML을 이용한 화면에 UI 표현하기
- 브라우저에서 UI를 볼 수 있는 것은 이 HTML을 분석해서 보여줄 수 있다.
- 이 HTML은 요소(Element)들로 구성되어 있다.

</details>