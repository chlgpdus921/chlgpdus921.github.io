---
title:  "자바스크립트 개념 정리"
excerpt: "자바 스크립트 개념 정리"
comments: true

categories:
  - basecamp
tags: 
  - [basecamp]
toc: true
toc_sticky: true
last_modified_at:  2021-01-21 03:15:00 +0000
---

## Goal

> - 자바 스크립트 기본 개념에 대해 이해한다. 
> - 모던 자바스크립트 책을 읽으며 새롭게 알게된 내용에 대해 작성했다.

---

## 3.2 웹 브라우저

- 크롬 개발자 도구 단축키(맥북 기준) : command + option + i

---

## 4장 변수

- **식별자** 
  - 어떤 값을 구별해서 식별할 수 있는 고유한 이름. 변수 이름을 식별자라고도 한다. 
  - 변수를 선언하고 값을 할당하지 않았을시 undefined 값이 암묵적으로 할당되어 초기화된다. 



- **자바스크립트** 
  - 소스코드 평가 과정 - 모든 선언문 (변수, 함수 선언문) 을 소스 코드에서 먼저 실행한다. (소스코드의 어디에 위치하는지와 상관없이 어디서든지 변수를 참조할 수 있다.)
    - = 변수 호이스팅 (variable hoisting)
    - 변수 선언은 런타임 이전에 실행되고, 값의 할당은 런타임에 실행된다. 

```javascript
console.log(score); // undefined

score = 80; // 값 할당
var score; // 변수 선언

console.log(score); // 80
```



- Const : 변수 재할당 금지 (상수)

```javascript
var score = 80;
score = 90;

//메모리 공간지우고, 메모리 공간에 재할당 값 90하는 것이 아님
//새로운 메모리 공간 확보하고, 그 공간에 90을 저장한다. 
//불필요한 값들은 가비지 콜렉터에 의해 메모리에서 자동 해제 된다. 
```



**Unmanaged language vs managed language**

**c언어** : Unmanaged language

개발자가 명시적으로 메모리를 할당하고 해제하기 위해 malloc(), free()

메모리 제어를 개발자가 주도할 수 있다. - 개발자의 역량에 따라 최적의 성능 확보 가능 but 치명적 오류 가능성 높아짐



**javascript** : managed language

개발자의 직접적인 메모리 제어 허용 x, 더이상 사용하지 않는 메모리 해제는 가비지 컬렉터가 수행.

일정한 생산성 확보 가능 but 성능면에서 어느정도 손실 감수해야함 



---

## 5장 표현식과 문

**리터럴 (literal)**

- 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법
- Ex) 정수, 부동소수점 2진수, 8진수, 16진수, 문자열, boolean, null, undefined, 객체, 배열, 함수, 정규표현식 



**표현식(expression) vs 문(statement)**

- 표현식 : 값으로 표현될수 있는 문 

```javascript
var score = 100;
10 + 20

```

- 문 : 프로그램을 구성하는 기본 단위이자 최소 실행 단위 
  - 선언문, 할당문, 조건문, 반복문 등으로 구분 할 수 있다. 
  - 문의 집합으로 이루어진 것이 프로그램, 문을 작성하고 순서에 맞게 나열하는 것이 프로그래밍이다. 



**Token** : 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소  

```javascript
// 문은 여러 토큰으로 구성된다.

var sum = 1 + 2; //문 (statement)
//Token : var, sum, =, 1, +, 2, ; 

```



---

## 6장 데이터 타입

문자열은 + 사용해 연결할 수 있다. 그 외의 경우는 덧셈 연산자로 동작한다.  

```javascript
var first = 'hye yeon'
var last = 'choi'

console.log('my name is' + first  + ' '+ last + '.');
console.log('my name is ${first} ${last}.');
```



null: 변수에 값이 없다는 것을 의도적으로 명시할 때 사용한다. 변수가 이전에  참조하던 값을 더 이상 참조하지 않겠다는 의미이다.  



데이터 타입이 필요한 이유

- 값을 저장할 때 확보해야하는 메모리 공간의 크기를 결정하기 위해 
- 값을 참조할 때 한 번에 읽어 들어야 할 메모리 공간의 크기를 결정하기 위해
- 메모리에서 읽어들인 2진수를 어떻게 해석할지 결정하기 위해                                        



자바 스크립트는 동적 타입 언어

- 변수가 선언이 아닌 할당에 의해 타입이 결정되는 것 

- 파이썬, PHP, Ruby, Perl 등



동적 타입 언어의 단점 

- 변수 값이 언제든지 변경될 수 있기 때문에 복잡한 프로그램에서는 변화하는 변수 값을 추적하기 어려울 수 있다.  
- 자바스크립트 엔진에 의해 암묵적으로 타이비 자동으로 변환되기도 한다. 
- 즉, 유연성은 높지만 신뢰성은 떨어진다. 



---

## 7장 연산자

```javascript
var x = '1';

console.log(+x); //문자열을 숫자로 타입 변환

x = true;
console.log(+x); //boolean을 숫자로 타입 변환

x = 'hello'
console.log(+x); //NaN
//문자열을 숫자로 타입 변환할 수 없으므로 NaN반환 
```



**비교 연산자**

| 비교 연산자 |    의미     |  사례   |           설명           |
| :---------: | :---------: | :-----: | :----------------------: |
|     ==      |  동등 비교  | x == y  |    x와 y의 값이 같음     |
|     ===     |  일치 비교  | x === y | x와 y의 값과 타입이 같음 |
|     !=      | 부동등 비교 | x != y  |    x와 y의 값이 다름     |
|     !==     | 불일치 비교 | x !== y | x와 y의 값과 타입이 다름 |

```javascript
5 == 5 //true
5 == '5' //true

5 === 5 //true
5 === '5' //false

NaN === NaN //자신과 일치하지 않는 유일한 값
isNaN(NaN) //true
```



**지수 연산자**

```javascript
2 ** 2; //4
Math.pow(2,2); //4
```



---

## 8장 제어문

**무한루프**

```javascript
for( ;;){
  
}

while(true){
  
}
```



---

## 9장 타입 변환과 단축 평가

**타입 변환이란?**

개발자가 의도적으로 값의 타입을 변환하는 것을 명시적 타입 변환, 타입 캐스팅 이라고 한다. 

자바스크립트 엔진에 의해 암묵적으로 타입이 자동변환 되는 것 . 암묵적 타입 변환, 타입 강제 변환



- **숫자 타입으로 변환**

```javascript
Number('1');
parseInt('1');
+ '1';
'101' * 1;
```

- **논리 연산자를 사용한 단축 평가**

```javascript
'Cat' && 'Dog' // "Dog" 출력
'Cat' || 'Dog' // "Cat" 출력
```

첫 번째 피연산자 'Cat'은 Truthy값이므로 true로 평가된다.

두 번째 피연사자가 결과를 결정한다. 이때 논리곱 연산자는 논리 연산의 결과를 결정하는 두 번째 피연산자 'Dog'를 그대로 반환한다. 



---

## 10장 객체 리터럴

**객체란?**

자바스크립트는 객체기반의 프로그래밍 언어.  객체는 프로퍼티와 메서드로 구성된 집합체다. 



**프로퍼티**

객체는 프로퍼티로 구성되며, 프로퍼티는 키와 값으로 구성된다.

```javascript
var person = {
	//프로퍼티 키 : name, 프로퍼티 값 : CHOI
    name : 'CHOI',

    //프로퍼티 키 : age, 프로퍼티 값 : 20
    age : 20

};

//프로퍼티 접근 방법
console.log(person.name);
console.log(person['name']);

//프로퍼티 값 갱신
person.name = 'kim';

//프로퍼티 동적 생성 - 동적으로 생성되고 값이 할당된다. 
person.lastname = 'hyeyeon' 

//프로퍼티 삭제
delete person.age;
delete person.address; //원래 없으므로 에러가 발생하지 않는다. 
```



**메서드 축약 표현**

```javascript
var obj = {
    name : 'choi',
    say : function(){
        console.log('hi');
    }
};

const obj = {
    name : 'choi',
    say(){
        console.log('hi');
    }
};
```



---

## 11장 원시 값과 객체의 비교

**문자열과 불변성**

- 다음과 같은 상황에서 world로 수정할 때, 참조된 메모리 공간을 수정하는 것이 아니다. 새로운 메모리에 'world'를 생성하고 식별자 str이 이것을 가리키는 것이다. 

```javascript
var str = 'hello';
str = 'world';

str[1] = 'p'; //변경 불가. 문자열은 읽기 전용 값이다. 
```



**값에 의한 전달**

```javascript
var score = 80;
var copy = score; //다른 메모리 공간에 저장된 별개의 값이다. 

console.log(score, copy); // 80 80 
console.log(score === copy); //True

score = 100;

console.log(score, copy); //100 80
console.log(score === copy); //false
```

 

**참조에 의한 전달** 

서로 같은 메모리 주소 값을 가리킴. 즉 두 개의 식별자가 하나의 객체를 공유한다. 

```javascript
var person = {
    name : 'CHOI',
    age : 20

};

//참조 값을 복사 (얕은 복사)
var copy = person; 

console.log(copy === person); //true

copy.name = 'kim';
person.address = 'seoul';

console.log(person); //{name : "kim", address : "seoul"}
console.log(copy); //{name : "kim", address : "seoul"}
```



---

## 12장 함수

**함수 리터럴**

- 함수도 객체 타입의 값이다. 함수 리터럴은 function 키워드, 함수 이름, 매개 변수 목록, 함수 몸체로 구성된다. 일반 객체는 호출할 수 없지만, 함수는 호출할 수 있다. 

```javascript
//변수에 함수 리터럴을 할당
var f = function add(x,y){
    return x + y;
}

//함수 선언식
function add(x,y){
    return x + y;
}

//함수 표현식
var f = function add(x,y){
    return x + y;
}

//Function 생성자 함수
var add = new Function('x', 'y', 'return x + y');

//화살표 함수
var add = (x,y) => x + y;
```



- 함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다. 

```javascript
var f = function add(x,y){
    return x + y;
}
//f : 식별자
//add : 함수 이름
console.log(f(2,5)); //7
```



**콜백 함수**

함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수

콜백 함수는 비동기처리 (이벤트 처리, Ajax 통신, 타이머 함수 등) 에 활용되는 중요한 패턴이다. 

```javascript
document.getElementById('myButton').addEventListener('click', function(){
    console.log('button clicked');
});

setTimeout(function(){
    console.log('1초 경과');
});
```



---

### Reference

이 글은 모던 자바스크립트 책을 보며 새롭게 알게 된 내용에 대해 작성했다.

[모던 자바스크립트 Deep Live](http://www.yes24.com/Product/Goods/92742567)





