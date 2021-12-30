## 변수(variable)
변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말한다.

## undefined
undifined는 자바스크립트에서 제공하는 원시 타입의 값(primitive value)이다.

## 변수 호이스팅
```javascript
console.log(score); // undefined
var score;  // 변수 선언문
```
변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 변수 호이스팅(variable hoisting)이라 한다.

```javascript
console.log(score);  // undefined

var score;  // 1. 변수 선언
score = 100;    // 2. 값의 할당

console.log(score); // 80
```
위 코드의 경우 실질적으로 아래와 같은 순서로 동작한다.

```javascript
var score;
console.log(score);
score = 100;
console.log(score);
```

그러니까 사실 이렇게 써도 동작을 함
```javascript
console.log(score);

score = 90;
var score;

console.log(score);
```