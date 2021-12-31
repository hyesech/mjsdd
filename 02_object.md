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