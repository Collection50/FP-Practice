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
