
### Nan( Not a Number) 값
```javascript
var foo = {
  name = 'foo',
  major = 'computer science'
};
```
#### 💡 이 상황에서 대괄호 표기법으로 foo['full-name'] = 'foo bar';로 동적 할당 후 console.log(foo.full-name); 시 undefined로 출력되는 이유

-----


자바스크립트에서 NaN(Not a number)은 수치 연산을 해서 정상적인 값을 얻지 못할 때 출력되는 값이다.

가령, 1-'hello' 라는 연산의 결과는 NaN이다. 1이라는 숫자와 문자열을 빼는 연산을 수행했기 때문이다.

앞의 코드에서 NaN이 출력된 이유는 우리가 프로퍼티에 접근하려는 의도와 다르게 foo.full과 name이라는 값을 -연산자로 계산하는 표현식으로 취급 했기 때문이다.

따라서 undefined-undefined의 연산 결과는 NaN이 되는것이다.
