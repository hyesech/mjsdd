## Object
자바스크립트를 구성하는 거의 모든 것. 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 모두 객체다.

원시 값은 변경 불가능한 값(immutable value)이지만 객체는 변경 가능한 값(mutable value)이다.

객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 key, value로 구성된다. 프로퍼티 값이 함수인 경우 이를 method라고 불러 구분한다. 

프로퍼티는 객체의 상태를 나타내는 값(data)이고, 메서드는 프로퍼티(state data)를 참조하고 조작할 수 있는 동작(behavior)이다. 

</br>

## 인스턴스
클래스에 의해 생성되어 메모리에 저장된 실체를 말한다. OPP에서 객체는 클래스와 인스턴스를 포함한 개념이다. 클래스는 인스턴스를 생성하기 위한 템플릿 역할을 한다.

</br>

## 메서드 축약 표현
```javascript
// ES5
var obj = {
    name: 'hyesech',
    sayHi: function() {
        console.log('Hi' + this.name);
    }
}
```

```javascript
// ES6
var obj = {
    name: 'hyesech',
    sayHi() {
        console.log('Hi' + this.name);
    }
}
```
이 경우 단순히 표현만 축약된 것이 아니라 둘의 동작은 다르다.

```javascript
// ES5
const a = new obj.sayHi();

// ES6
const b = new obj.sayHi();
```
a의 경우 위와 같이 바로 사용이 가능. b의 경우 constructor가 없기 때문에 위와 같은 방식으로는 사용 불가. 그러니까 조금 더 메서드로서 사용하는 것이 옳다. 


## 원시값과 객체의 배교
```javascript
var score = 80;

// 0xc000000A2 -> 식별자: score, 값: 0x00000F2 (undefined)
// 0xc000000A2 -> 식별자: score, 값: 0x000001332 (80)

score = 90;
// 0xc000000A2 -> 식별자: score, 값: 0x00000F913 (90)
```

즉 식별자가 선언된 주소가 존재하고, 값이 재할당 될 때마다 참조하는 메모리의 주소가 변경된다. 80, 90은 식별자와 동일한 메모리 주소에 저장된 것이 아니라 별개의 주소에 저장되어 있는 독립적인 데이터이다. score라는 식별자를 가지고 있는 값이 변경된다는 것은 참조하는 메모리 주소가 변경되는 것이다. undefined도 그렇고 원시 값의 경우 한 번 만들어지면 그대로 유지된다. 값이 변경되지 않음.

</br>

## 문자열과 불변성
```javascript
var str = 'Hello';
str = 'world';
```
위와 같이 식별자 str에 'Hello'라는 문자열을 할당했다가 'world'를 재할당하는 경우, 메모리 영역에서는 어떤 일이 일어나나? 

일반적으로 원시값은 원시 타입별로 메모리 공간의 크기가 미리 정해져 있다. C의 경우 문자열 타입은 존재하지 않는다. 하나의 문자를 위한 데이터 타입(char)만 존재한다. 문자열은 배열로 처리하고, 자바에서는 문자열을 String 객체로 처리한다.

자바스크립트는 편의를 위해 원시 타입인 문자열 타입을 제공한다. 따라서 자바스크립트에서 문자열은 원시 타입이며, 변경 불가능하다. 이는 문자열이 생성된 이후에는 변경할 수 없음을 의미한다.

문자열은 유사 배열 객체라고 한다. 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고, length 프로퍼티를 갖는다. 인덱스를 통해 각 문자에 접근할 수 있고, for문으로 순회할 수도 있다. 

String의 프로토타입을 확인해보면 `Symbol(Symbol.iterator)`가 있음. 즉 이터러블함. 

```javascript
var str = 'string';
str[0] = 'S';

console.log(str);        // string
```
따라서 위와 같이 값을 변경한다고 해서 문자열이 변경되는 것은 아니다. 다만 에러가 발생하지는 않는다. 한 번 생성된 문자열은 읽기 전용 값으로 변경할 수 없는 값이며, 예기치 못한 변경으로부터 자유롭다. 

변수에 새로운 문자열을 할당하는 것은 가능하다. 기존 문자열을 변경하는 것이 아니라, 새로운 문자열을 새롭게 할당하는 것이기 때문. 

```javascript
str.slice(2,3);
```
위와 같은 작업을 하면 사실상 다음과 같이 동작한다.

```javascript
str.slice(2,3);
const tempStr = new String(str);
tempStr.slice(2,3);
```
인스터를 만들어서 메소드를 적용한 다음 원하는 값을 반환하고 가비지 컬렉팅 진행한다고 보면 이해가 쉽다. 임시로 래퍼 객체를 만들어서 메서드를 적용하고 폐기.

프로토타입 자체도 배열이 아니가 String임.

</br>

## 값에 의한 전달(call by value)
```javascript
var score = 80;
var copy = score;

console.log(score);     // 80
consold.log(score);     // 80

score = 100;

console.log(score);     // 100
console.log(copy);      // ?
```
위의 경우 기댓값은 무엇인가? 80이다. 
원시값은 불변하다. line2에서 copy에 score가 할당되었고(복사) 이 때 copy는 score가 참조하고 있는 원시값 메모리 주소를 참조하게 된다. line7에서 score에 100을 할당하면 score는 새로운 원시값인 100의 메모리 주소를 참조하게 되고, copy는 그대로 기존에 참조하던 위치를 참조한다. 원시값은 불변이기 때문이다. score의 값을 변경한 것은 실제 값을 변경한 것이 아니라 참조하는 메모리 주소가 변경된 것이므로 80과 100은 별개의 주소에 저장되어 있다. 

> 엄격하게 표현하면 변수에는 값이 전달되는 것이 아니라 메모리 주소가 전달되기 때문이다. 이는 변수와 같은 식별자는 값이 아니라 메모리 주소를 기억하고 있기 때문이다.

</br>

## 객체
객체는 프로퍼티의 개수가 정해져 있지 않고, 동적으로 추가되고 삭제할 수 있다. 프로퍼티의 값에도 제약이 없다. 따라서 객체는 원시 값과 같이 확보해야 할 메모리 공간의 크기를 사전에 정의할 수 없다.

객체는 복합적인 자료구조이므로 객체를 관리하는 방식이 원시 값과 비교해서 복잡하고 구현 방식도 브라우저 제조사마다 다를 수 있다. 객체를 생성하고 프로퍼티에 접근하는 것도 원시값과 비교할 때 비용이 많이 드는 일이다. 따라서 객체는 원시 값과는 다른 방식으로 동작하도록 설계되어 있다.

자바스크립트 객체는 프로퍼티 키를 인덱스로 사용하는 해시 테이블(hash table - 연관 배열, map, dictionary, lookup lable)이라고 생각할 수 있다. 대부분의 자바스크립트 엔진은 해시 테이블과 유사하지만 높은 성능을 위해 일반적인 해시 테이블보다 나은 방법으로 객체를 구현한다.

클래스 기반 OPP 언어는 사전 정의된 클래스를 기반으로 객체(인스턴스)를 생성한다. 객체 생성 이전에 이미 프로퍼티와 메서드가 정해져 있으며 그대로 객체를 생성하는 것임. 객체가 생성된 이후에는 프로퍼티를 삭제, 추가할 수 없다. 하지만 자바스크립트는 클래스 없이 객체를 생성할 수 있으며 객체가 생성된 이후라도 동적으로 프로퍼티와 메서드를 추가할 수 있다. 이론적으로 클래스 기반 OPP 언어의 객체보다 생성과 프로퍼티 접근에 비용이 더 많이 드는 비효율적인 방식이다. 따라서 V8 자바스크립트 엔진에서는 프로퍼티에 접근하기 위해 동적 탐색(dynamic lookup) 대신 히든 클래스(hidden class)라는 방식을 사용한다. 히든 클래스는 자바와 같이 고정된 객체 레이아웃(클래스)과 유사하게 동작한다. 

```javascript
var person = {
    name: 'hyesech'
};
```
한 단계가 더 있다고 보면 좋을 것 같다. mutable이 되기 위해서는 참조를 할 수밖에 없음. 객체를 할당한 변수의 경우 '변수는 객체를 참조하고 있다.' 또는 '변수는 객체를 가리키고(point) 있다.'고 표현한다. 즉 person이라는 식별자를 갖는 변수는 { name: 'hyesech' }를 가리키고(참조하고) 있다.

더블 포인터라고 할 수 있나...? 한 단계를 더 거치니까 참조형이 되는 것임. 한 개만 거치면 불변성ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ

참조형도 불변하게 만들 수는 있다. 
```javascript
var person = {
    name: 'hyesech'
}

person = { age: 90 };
```
이 경우는 객체를 갈아 치운 경우다. 그러니까 기존의 객체를 건드린 것이 아니라 그냥 새로운 객체를 재할당 해버린 것임. 이것이 불변 객체임. `Object.freeze()`를 이용해서 객체를 얼려버릴 수도 있지만, 이 개념이 아님.

```javascript
person.name = 'ch';          // X
person = { name: 'ch' }     // O
```
이처럼 아예 객체 자체를 변경해버리는 것을 말한다. 혹은 line1과 같이 코드를 작성했을 때 프록시를 이용해서 line2와 같이 동작하도록 만들 수도 있음. 그런 라이브러리를 쓰는 한은 불변 객체를 유지할 수 있는 것임. 그게 immer였던가? 아무튼. 불변 객체라는 것은 객체를 다루는 기법임.

</br>

## 얕은 복사와 깊은 복사(shallow copy and deep copy)
상대적인 개념이 아님. 객체의 경우 얕은 복사는 한 단계까지만 복사하는 것을 말하고, 깊은 복사는 객체에 중첩되어 있는 객체까지 모두 복사하는 것을 말한다.

```javascript
const o = { x: { y: 1 } };

// shallow copy
const c1 = { ...o };
console.log(c1 === o)            // false
console.log( cl.x === o.x )     // true

 // lodash의 cloneDeep을 사용한 deep copy
 const _ = require('lodash');

 // deep copy
 const c2 = _.cloneDeep(o);
 console.log(c2 === o);          // false
 console.log(c2.x === o.x)      // false  
```
얕은 복사와 깊은 복사로 생성된 객체는 원본과는 다른 객체다. 원본과 복사본이 참조하고 있는 주소는 다르다. 하지만 얕은 복사는 객체에 중첩되어 있는 객체의 경우 참조값을 복사하고, 깊은 복사는 객체에 중첩되어 있는 객체까지 모두 복사해서 원시 값처럼 완전한 복사본을 만든다는 차이가 있다. 

중첩 객체인 경우 깊은 복사를 이용해야 불변 객체를 만들 수 있다.

```javascript
// 깊은 복사 X
var a = { a: [1, 2, 3] };
var b = a;

console.log(a === b);       // true

a.a[0] = 4;
console.log(b.a[0])          // 4
```

```javascript
// 깊은 복사 O
var a = { a: [1, 2, 3] };
var b = { a: [...a.a] };

console.log(a === b);       // false

a.a[0] = 5;
console.log(b.a[0])          // 1
```
값에 의한 전달과 참조에 의한 전달은 식별자가 기억하는 메모리 공간에 저장되어 있는 값을 복사해서 전달한다는 면에서 동일하다. 다만 식별자가 기억하는 메모리 공간, 즉 변수에 저장되어 있는 값이 원시 값이나 참조 값이냐의 차이만 있을 뿐이다. 따라서 자바스크립트에는 참조에 의한 전달은 존재하지 않고, 값에 의한 전달만이 존재한다고 말할 수 있다.

```javascript
var person1 = {
    name: 'hyesech'
}

var person2 = {
    name: 'hyesech'
}

console.log(person1 === person2);       // (1)
console.log(person1.name === person2.name)      // (2)
```
위의 경우 (1)은 false, (2)는 true다. 