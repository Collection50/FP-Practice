# ES6의 순회와 이터러블

## 기존과 달라진 ES6 리스트 순회

- `for i++`
- `for of`

```js
// ES5
const list = [1, 2, 3];
for (var i = 0; i < list.length; i++) {
  console.log(list[i]);
}

const str = 'abcdefg';
for (var i = 0; i < list.length; i++) {
  console.log(list[i]);
}
```

```js
// ES6 이후
const list = [1, 2, 3];
for (const a of list) {
  console.log(a);
}
```

## Array, Set, Map을 통해 알아보는 이터러블/이터레이터 프로토콜

- Well-Formed 이터레이터: 이터레이터가 자기 자신을 반환하는 이터레이터를 가지고 있을 때

### Array

```js
const arr = [1, 2, 3];
for (const num of arr) {
  console.log(num);
}
```

### Set

```js
const set = new Set([1, 2, 3]);
for (const num of set) {
  console.log(num);
}
```

### Map

```js
const map = new Map([
  ['a', 1],
  ['b', 2],
  ['c', 3],
]);
for (const num of map) {
  console.log(num);
}
for (const num of map.values()) {
  console.log(num);
}
for (const num of map.keys()) {
  console.log(num);
}
```

## 이터러블/이터레이터 프로토콜

- 이터러블: 이터레이터를 리턴하는 `[Symbol.iterator]()`를 가진 값
- 이터레이터: `{ value, done }` 객체를 리턴하는 `next()`를 가진 값 (next 함수)
- 이터러블/이터레이터 프로토콜: 이터러블을 `for...of`, `스프레드 문법`을 사용할 수 있도록 작성된 규칙

## 사용자 정의 이터러블을 통해 알아보기

```js
// Well-Formed 이터레이터가 아닌 경우
const iterable = {
  [Symbol.iterator]() {
    let i = 3;
    return {
      next() {
        return i === 0 ? { done: true } : { value: i--, done: false };
      },
    };
  },
};

// Well-Formed 이터레이터인 경우
const WFIterable = {
  [Symbol.iterator]() {
    let i = 3;
    return {
      next() {
        return i === 0 ? { done: true } : { value: i--, done: false };
      },
      [Symbol.iterator]() {
        return this;
      },
    };
  },
};
```

## 이터러블을 활용할 수 있는 것들

- 이터러블/이터레이터 프로토콜이 구현되어 있는 것들
- `Array`, `Set`, `Map`, `Brower APIs`, 전개 연산자 등

```js
for (const element of document.querySelectorAll('*')) {
  console.log(element);
}

const all = document.querySelectorAll('*');
const iter = all[Symbol.iterator]();
console.log(iter3.next());
```

## 전개 연산자 (스프레드 문법)

- 이터러블 프로토콜 사용

```js
const array = [1, 2];
console.log(...array);
```
