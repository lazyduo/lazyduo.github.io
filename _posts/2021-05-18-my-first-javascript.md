---
title: "Javascript 첫 느낌"
date: 2021-05-18 23:56:00 +0900
classes: wide
toc: true
tags:
    - tech
    - javascript
    - web design
---

대세?를 따르기 위해 'React Native' tuotorial을 펼쳤다가, 'React'하고 오래서 갔더니 'javascript' 보고 오래서 문법만 슬쩍 본 내용입니다.

Django 개발하면서 자바스크립트로 Ajax도 사용했었지만, 딱히 문법을 따로 보지 않고 그냥 돌아다니는 코드 수정해서 쓰는 식으로 사용했었습니다. 언젠간 해야할건데 왜 미뤘는지 모르겠습니다. (바빠서..)

[참고 링크](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)

위 링크는 React 튜토리얼에서 잠깐 보고 오기 좋다고 추천해 준 사이트 입니다. 잘 정리되어 있습니다.

## 정리

개인적으로 python, c/c++ 대비 특이해서 메모할 용도로 작성하였습니다.

### Numbers

- parseInt / isNan() / isFinite()

    ```javascript
    parseInt('123', 10); // 123
    parseInt('010', 10); // 10
    parseInt('010');  //  8
    parseInt('0x10'); // 16
    parseInt('11', 2); // 3

    Number.isNaN(NaN); // true
    Number.isNaN('hello'); // false
    Number.isNaN('1'); // false
    Number.isNaN(undefined); // false
    Number.isNaN({}); // false
    Number.isNaN([1]) // false
    Number.isNaN([1,2]) // false

    isFinite(1 / 0); // false
    isFinite(-Infinity); // false
    isFinite(NaN); // false
    ```

    - Infinity 가 cnst로 있음

### Strings

```javascript
'hello'.length; // 5
'hello'.charAt(0); // "h"
'hello, world'.replace('world', 'mars'); // "hello, mars"
'hello'.toUpperCase(); // "HELLO"
```

### Variables

선언하는 방법에는 `let`, `const`, `var`가 있음.

`let`과 `var`의 차이점 : `let`은 블록 내에서만 유효하다.

```javascript
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // 상위 블록과 같은 변수!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // 상위 블록과 다른 변수
    console.log(x);  // 2
  }
  console.log(x);  // 1. 위의 if 문에서의 let이 먹히지 않는다.
}
```

### Operators

'=='은 type이 달라도 같다고 인식한다. 그래서 '==='을 쓴다.

```javascript
123 == '123'; // true
1 == true; // true

123 === '123'; // false
1 === true;    // false
```


### Control Structures

if, if else, for, while, switch 등 C/C++과 동일

### Objects

Python의 Dictionary와 사용법과 기능이 거의 같고, JSON 형식으로 써 내려가면 된다.

```javascript
var obj = {
    name: 'Carrot',
    _for: 'Max', // 'for' is a reserved word, use '_for' instead.
    details: {
        color: 'orange',
        size: 12
    }
};
```

### Arrays

Python의 List와 거의 같다. 특이한 점은 `a[100]`이 뜬금없이 바로 먹힌다. 그 사이 인덱스들의 값은 undefined 처리 된다.

```javascript
var a = ['dog', 'cat', 'hen'];
a[100] = 'fox';
a.length; // 101
typeof a[90]; // undefined
```
- a.push(), a.pop() 등 사용 가능

### Functions

기본형

```javascript
function add(x, y) {
var total = x + y;
return total;
}
```

특이한 점은 Python의 *args처럼 `...args(arguments)`로 변수를 넣을 수 있다.

```javascript
function avg(...args) {
var sum = 0;
for (let value of args) {
    sum += value;
}
return sum / args.length;
}

avg(2, 3, 4, 5); // 3.5
```

- array를 argument로 바꾸려면 `apply()`를 사용한다.

```javascript
avg.apply(null, [2, 3, 4, 5]); // 3.5
```

### Custom Objects

자바스크립트는 클래스 객체가 없는 대신, Function으로 그 기능을 대체한다.

```javascript
function Person(first, last) {
this.first = first;
this.last = last;
this.fullName = function() {
    return this.first + ' ' + this.last;
};
this.fullNameReversed = function() {
    return this.last + ', ' + this.first;
};
}
var s = new Person('Simon', 'Willison');
```

`object.prototype.function`으로 object에 아무때나 function을 추가해 줄 수 있다. 이는 String등의 이미 기본으로 있는 객체에 함수를 추가해 줄 때 유용하다.

```javascript
var s = 'Simon';
s.reversed(); // TypeError on line 1: s.reversed is not a function

String.prototype.reversed = function() {
var r = '';
for (var i = this.length - 1; i >= 0; i--) {
    r += this[i];
}
return r;
};

s.reversed(); // nomiS
```

### Closures

잘 안쓸것 같은 기능. 이중 함수? 이상한 개념이다.

```javascript
function makeAdder(a) {
return function(b) {
    return a + b;
};
}
var add5 = makeAdder(5);
var add20 = makeAdder(20);
add5(6); // 11
add20(7); // 27
```
