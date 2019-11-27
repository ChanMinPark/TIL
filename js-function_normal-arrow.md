# [Javascript] 일반함수와 화살표 함수(arrow function)의 차이  

일반함수와 화살표 함수(arrow function)의 차이에 대해서 알아봅니다.

ES6 이전에는 함수를 선언하기 위해서 함수선언식, 함수표현식 방식을 사용했습니다.  
ES6에서는 새로운 함수 선언 방식으로 화살표 함수가 등장했습니다.  

기존의 일반함수들은 function 키워드를 이용해서 함수를 선언하지만, 화살표 함수는 이름처럼 화살표 키워드를 이용합니다.  
```js
// 함수표현식
let function1 = function () {
  console.log('함수표현식');
}
// 함수선언식
function function2 () {
  console.log('함수선언식');
}

// 화살표 함수
let function3 = () => {
  console.log('화살표 함수');
}
```

일반함수와 화살표 함수는 크게 3가지 다른 점이 있습니다.  

## 차이점 1: this
화살표 함수와 기존의 일반함수는 this가 다른 곳을 가리킵니다.  
화살표 함수의 this는 바로 상위 스코프의 this와 같습니다. 하지만 기존의 일반함수는 this가 동적으로 바인딩됩니다.  
일반함수의 this는 아래와 같습니다.  
- 내부함수, 콜백 함수: 전역 객체(브라우저에서는 window, node에서는 global)  
- 객체의 메소드: 메소드를 소유한 객체 자체  
- 생성자 함수: 생성자로 생성하는 객체  


## 차이점 2: 생성자 함수로 사용 가능 여부  
일반함수는 생성자 함수로 사용할 수 있지만, 화살표 함수는 생성자 함수로 사용할 수 없습니다.  
화살표 함수는 prototype 프로퍼티를 가지고 있지 않기 때문입니다.  


## 차이점 3: arguments 사용 가능 여부  
일반함수에서는 함수가 실행될 때 암묵적으로 arguments 변수가 전달되어 사용할 수 있었지만, 화살표 함수에서는 arguments 변수가 전달되지 않습니다.  


화살표 함수가 새로 나왔다고 해서 무조건 모든 상황에 좋은 건 아닌것 같습니다.  
필요에 따라서 적절하게 함수를 만들어야겠습니다.  

### 참고자료  
- https://poiemaweb.com/es6-arrow-function  
- http://webframeworks.kr/tutorials/translate/arrow-function  
- https://poiemaweb.com/js-this  
