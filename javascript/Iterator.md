# Iterator


## TL;DR
    이터레이터 프로토콜은 next 메소드를 소유하며 next 메소드를 호출하면 이터러블을 순회하며 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환하는 것이다. 이 규약을 준수한 객체가 이터레이터이다.




## 이터레이션 프로토콜
     이터레이션 프로토콜(iteration protocol)은 데이터 컬렉션을 순회하기 위한 프로토콜(미리 약속된 규칙)이다    

### 1. 이터러블 프로토콜
    - Array, String, Map, Set, Arguments, TypeArray
    - Symbol.iterator 메소드를 구현하거나 프로토타입 체인에 의해 상속한 객체
    - Symbol.iterator 메소드는 이터레이터
    - 이터러블은 for…of 문에서 순회할 수 있으며 Spread 문법의 대상으로 사용할 수 있다.
```js
const array = [1, 2, 3];

// 배열은 Symbol.iterator 메소드를 소유한다.
// 따라서 배열은 이터러블 프로토콜을 준수한 이터러블이다.
console.log(Symbol.iterator in array); // true

// 이터러블 프로토콜을 준수한 배열은 for...of 문에서 순회 가능하다.
for (const item of array) {
  console.log(item);
}
```

이터러블 객체를  Symbol.iterator를 이용하여 이터레이터로 만들 수 있습니다.
```js
// 배열은 이터러블 프로토콜을 준수한 이터러블이다.
const array = [1, 2, 3];

// Symbol.iterator 메소드는 이터레이터를 반환한다.
const iterator = array[Symbol.iterator]();

// 이터레이터 프로토콜을 준수한 이터레이터는 next 메소드를 갖는다.
console.log('next' in iterator); // true

```


### 2. 이테레이터 프로토콜
    - 이터레이터


## intro
반복을 위해 설계된 특정 인터페이스가 있는 객체이다. 

Iterator는 컬렉션 내부 위치에 대한 내부 포인터를 유지하고 next()메서드를 호출할 때마다 다음 값을 반환합니다.

마지막 값이 반환된 후에 next()를 호출하면 메서드는 done을 true로 리턴하고 value는 Iterator의 리턴 값을 포함합니다. 이 리턴 값은 데이터의 일부가 아니며 관련 데이터의 마지막 부분이거나 그러한 데이터가 없으면 undefined가 됩니다. Iterator의 리턴 값은 정보를 호출자에게 전달하는 마지막 방법이라는 점에서 함수의 리턴값과 유사합니다.

## The iterator protocol

iterator protocol은 value들의 sequence를 만드는 표준 방법을 정의합니다.

객체가 next()메소드를 가지고 있고 아래의 규칙에 따라 구현되어있으면 객체는 iterator입니다.

간단히 말하면 반복가능한 타입으로 정의할 수 있다. 

컬렉션에 다음항목을 반환하는게 기본이다.

next()은 다음 프로퍼티를 가지는 객체를 반환합니다.

1. done(boolean) 
    - Iterator가 마지막 반복작업을 마쳤을 true.만약 iterator에 return값이 있다면 value의 값으로 지정된다.
    - Iterator의 작업이 남아있는 경우 false이거나  done프로퍼티 할당이 생략될 수 있다.
2. value
    - Iterator로부터 반환되는 모든 자바스크립트 값이며 done이 true인 경우 생략될 수 있다.

## 1. 내장 iterables

String, Array, TypedArray, Map, Set

이 객체들의 프로토타입 객체들은 모두 @@iterator 메소드를 가지고 있다

## 2. 사용자 정의 iterable
```js
var myIterable = {};
myIterable[Symbol.iterator] = function* () {
    yield 1;
    yield 2;
    yield 3;
};
[...myIterable]; // [1, 2, 3]
```
## 3. Iterable을 허용하는 내장 API

- Map([iterable])
- WeakMap([iterable])
- Set([iterable])
- WeakSet([iterable])
- Promise.all(iterable)
- Promise.race(iterable)
- Array.from()

## 4. Iterable과 함께 사용되는 분법

- for-of
- spread operator
- yield*
- destructuring assignment
```js
// for-of
for(let value of ["a", "b", "c"]){
    console.log(value);
}

// spread operator
[..."abc"];

// yield*
function* gen(){
    yield* ["a", "b", "c"];
}

gen().next(); 

// destructuring
[a, b, c] = new Set(["a", "b", "c"]);
```

## 5. 예시
```js
//기본적인 iterator
function makeIterator(array){
    var nextIndex = 0;
    
    return {
        next: function(){
            return nextIndex < array.length ?
                {value: array[nextIndex++], done: false} :
                {done: true};
        }
    };
}

var it = makeIterator(['yo', 'ya']);

console.log(it.next().value); // 'yo'
console.log(it.next().value); // 'ya'
console.log(it.next().done);  // true

//Generartor를 이용한 iterator
function* makeGenerator(array){
    var nextIdx = 0;

    while(nextIdx < array.length){
        yield array[nextIdx++];
    }
}

var gen = makeGenerator(['yo', 'ya'])
console.log(gen.next().value); // 'yo'
console.log(gen.next().value); // 'ya'
console.log(gen.next().done);  // true
```
## REF
- [poiemaweb](https://poiemaweb.com/es6-iteration-for-of)
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols)
- [https://github.com/qodot/wiki/blob/master/js/es6-iterator.md](https://github.com/qodot/wiki/blob/master/js/es6-iterator.md)
- [http://hacks.mozilla.or.kr/2015/08/es6-in-depth-generators/](http://hacks.mozilla.or.kr/2015/08/es6-in-depth-generators/)
- [http://hacks.mozilla.or.kr/2016/02/es6-in-depth-generators-continued/](http://hacks.mozilla.or.kr/2016/02/es6-in-depth-generators-continued/)