# [Javascript] Prototype에 대해서 알아봅니다.  

## Prototype(또는 Prototype Object) 이란?  
자바스크립트에서 함수를 만들면 함께 생성되는 객체가 Prototype(또는 Prototype Object)입니다.  
그리고 해당 함수의 'prototype'이라는 속성으로 Prototype Object와 연결됩니다.  

개인적인 생각으로는 Java에서, class 내부의 static member와 유사하다고 생각합니다.  

## Prototype의 목적  
Prototype Object는 생성자 함수에 의해 생성된 각각의 객체에 공유 프로퍼티를 제공하기 위해 사용합니다.  
간단한 예시를 들면 아래와 같습니다.  

```js
function Car () {}

Car.prototype.wheel = 4;
Car.prototype.sideMirror = 2;

let smallCar  = new Car ();
let bigCar = new Car ();

console.log('smallCar :: wheel count = ', smallCar.wheel);
console.log('smallCar :: side mirror count = ', smallCar.sideMirror);
console.log('bigCar :: wheel count = ', bigCar.wheel);
console.log('bigCar :: side mirror count = ', bigCar.sideMirror);
// [ 출력 ]
// smallCar :: wheel count =  4
// smallCar :: side mirror count =  2
// bigCar :: wheel count =  4
// bigCar :: side mirror count =  2
```

smallCar와 bigCar는 크기가 다를 뿐 둘다 자동차입니다. 자동차이기 때문에 공통적으로 가지고 있는 속성들이 있는데, 이를 smallCar와 bigCar에 각각 만들어주기보다 Car의 Prototype Object에 만들어두면 메모리에 같은 정보를 중복으로 저장시키지 않기 때문에 메모리 효율적이며, 이런 공통적인 속성의 값을 바꿀때 모든 객체의 값을 바꾸지 않고 Prototype Object에 있는 값만 바꿔주면 되어 편리합니다.  

## Prototype Object에 접근하기  
위의 예시를 토대로 Prototype에 접근하는 방법을 알아보면,  
Car.prototype 또는 smallCar.__proto__ / bigCar.__proto__ 를 이용해서 Prototype Object에 접근할 수 있습니다.  
즉, {생성자함수}.prototype 또는 {객체}.__proto__ 가 Prototype Object를 가리킵니다.  


### 참고자료  
- https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67  
