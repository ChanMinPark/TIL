# [Javascript] var, let, const에 대해서 알아봅니다


var, let, const는 javascript에서 변수를 선언할 때 사용하는 키워드입니다.  

## var  
ES6 이전에는 변수를 선언할 때 var 키워드를 사용했습니다.  
우선, var 키워드는 아래와 같은 특징을 가지고 있습니다.  
- 변수의 중복 선언이 가능하다.  
- var 키워드는 생략이 가능하다.  
- block-scope이 아닌 function-scope이다.  
- 호이스팅(hoisting) 당한다.  

```js
/*
 * function-scope과 block-scope의 차이
 */

// function-scope
for (var i = 0; i < 10; i++) {
  console.log(i);
}
console.log('outside i: ', i); // 출력: outside i:  10
// i를 var로 선언 했기 때문에 function-scope를 사용해서 for문에 선언한 i가 정상적으로 값을 가지고 있다.

// block-scope
for (let i = 0; i < 10; i++) {
  console.log(i);
}
console.log('outside i: ', i); // 출력: Uncaught ReferenceError: i is not defined
// i를 let으로 선언하면 block-scope을 사용해서 for문 밖에서는 사용할 수 없다.
```

```js
/*
 * hoisting (호이스팅) 예시
 */

// 작성 코드
for (var i = 0; i < 10; i++) {
  console.log(i);
}

// 호이스팅 된 코드
var i
for (i = 0; i < 10; i++) {
  console.log(i);
}
```

위와 같은 특징을 가진 var는 변수의 사용에 대해서 다른 프로그래밍 언어와 다른 동작을 하는 이슈가 있었습니다. 잘 알고 일부러 쓰면 유용하게 사용할 수 있지만, 모르고 사용하면 스크립스 수행 간에 오류가 야기 될 수 있습니다.  

오류 예 1. 한번 선언한 변수를 모르고 다시 선언 해서 다른 목적으로 사용할 때, 오류가 나지 않는다.  
오류 예 2. 호이스팅으로 인해서, 변수 선언 이전에 변수를 사용하더라도 에러가 발생하지 않는다.  


이로 인해서 ES6에서는 변수 선언 키워드로 새롭게 let과 const를 만들었습니다.  

## let  
let은 아래와 같이 var와 다른 특징이 있습니다.  
- 중복 선언 불가.  
- block-scope (* const도 동일)  
- 값의 할당 이전에 선언이 반드시 되어 있어야한다.  

## const  
var의 단점을 피하기 위해서 let 하나만 있어도 될 것 같지만, const도 그것 만의 특징이 있습니다.  
- immutable 변수를 만든다.  
- 재선언, 재할당 모두 불가.  
- 선언과 할당이 반드시 동시에 이뤄져야한다.  

이로써, ES6에서는 변수의 선언에 사용하는 키워드가 여러개이므로 목적에 따라서 알맞게 사용하여야하겠습니다.  


### 참고자료  
- https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d  
- https://evan-moon.github.io/2019/06/18/javascript-let-const