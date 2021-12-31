## 비교 연산자: 동등 비교
타입 형변환을 암묵적으로 수행하고 동등한 경우 true, 다른 경우 false를 반환한다. 

</br>

## 비교 연산자: 일치 비교
될 수 있으면 동등 비교보다는 일치 비교를 사용함. 일치 비교 연산자는 좌항과 우항의 피연산자가 타입도 같고, 값도 같은 경우에 한하여 true를 반환한다. 암묵적 타입 변환을 하지 않음.

다만 NaN을 주의해야 하는데,

```javascript
NaN === NaN     // false
```
NaN은 자신과 일치하지 않는 유일한 값이다. 따라서 숫자가 NaN인지 조사하려면 isNaN을 사용해야 한다.

그런데, isNaN도 문제가 있다. 

```javascript
isNaN(NaN)                 // true
isNaN(undefined)        // true
isNaN({})                     // true
```
그래서 `Number.isNaN()`을 사용하는 것이 좋다. ES6에 나온 것임. 
