## 즉시 실행 함수
함수 정의와 동시에 즉시 호출되는 함수(IFE: Immediately Invoked Fucntion Expressiong). 즉시 실행되는 함수는 단 한 번만 호출되며 다시 호출할 수 없다.

```javascript
(function () {
    var a = 3;
    var b = 5;
    return a*b;   
}()) 
```
이 경우 기명으로 식별자를 붙여보아야 도움이 아 딘다.,