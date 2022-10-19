## 맵과 셋

- 맵(Map)과 셋(Set)자료형은 객체, 배열을 보완하기 위해 등장한 자료형이다.

## 맵

- 맵은 **키가 있는 데이터를 저장한다**는 점에서 객체와 유사하다. 다만, 맵은 키에 다양한 자료형을 허용한다는 점에서 차이가 있다. 

#### 맵의 메서드와 프로퍼티

`new Map()` – 맵을 만든다.
`map.set(key, value)` – key를 이용해 value를 저장한다.
`map.get(key)` – key에 해당하는 값을 반환한다. key가 존재하지 않으면 undefined를 반환한다.
`map.has(key)` – key가 존재하면 true, 존재하지 않으면 false를 반환한다.
`map.delete(key)` – key에 해당하는 값을 삭제한다.
`map.clear()` – 맵 안의 모든 요소를 제거한다.
`map.size` – 요소의 개수를 반환한다.

```js
let map = new Map();

map.set('1', 'str1');   // 문자형 키
map.set(1, 'num1');     // 숫자형 키
map.set(true, 'bool1'); // 불린형 키

// 맵은 키의 타입을 변환시키지 않고 그대로 유지한다.
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```

- 맵은 객체와 달리 키를 문자열로 변환하지 않는다.
- 맵은 객체와 달리 객체키를 사용할 수 있다.

#### 맵 체이닝

- `map.set`을 호출할 때마다 맵 자신이 반환되므로, 이를 이용해 체이닝을 할 수 있다.

```js
map.set('1', 'str1')
  .set(1, 'num1')
  .set(true, 'bool1');
```

#### 맵의 요소에 반복작업하기

`map.keys()` – 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환한다.
`map.values()` – 각 요소의 값을 모은 이터러블 객체를 반환한다.
`map.entries()` – 요소의 [키, 값]을 한 쌍으로 하는 이터러블 객체를 반환합니다. 이 이터러블 객체는 for..of반복문의 기초로 쓰인다.

```js
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);

// 키(vegetable)를 대상으로 순회
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// 값(amount)을 대상으로 순회
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// [키, 값] 쌍을 대상으로 순회
for (let entry of recipeMap) { // recipeMap.entries()와 동일합니다.
  alert(entry); // cucumber,500 ...
}
```

#### 맵 <-> 객체 변환

`Object.entries()` - 객체를 맵으로 변환
`Object.fromEntries()` - 맵을 객체로 변환

```js
let prices = Object.fromEntries([
  ['banana', 1],
  ['orange', 2],
  ['meat', 4]
]);

// now prices = { banana: 1, orange: 2, meat: 4 }

alert(prices.orange); // 2

let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map.entries()); // 맵을 일반 객체로 변환 (*)

// 맵이 객체가 되었습니다!
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2

```

## 셋

- 중복을 허용하지 않는 값을 모아놓은 컬렉션으로, 키가 없는 값이 셋에 저장된다.

#### 셋의 주요 메서드

`new Set(iterable)` – 셋을 만든다. `이터러블` 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 넣어준다.
`set.add(value)` – 값을 추가하고 셋 자신을 반환한다.
`set.delete(value)` – 값을 제거합니다. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 true, 아니면 false를 반환한다.
`set.has(value)` – 셋 내에 값이 존재하면 true, 아니면 false를 반환한다.
`set.clear()` – 셋을 비운다.
`set.size` – 셋에 몇 개의 값이 있는지 세준다.

`set.keys()` – 셋 내의 모든 값을 포함하는 이터러블 객체를 반환한다.
`set.values()` – set.keys와 동일한 작업을 합니다. 맵과의 호환성을 위해 만들어진 메서드이다.
`set.entries()` – 셋 내의 각 값을 이용해 만든 [value, value] 배열을 포함하는 이터러블 객체를 반환한다. 맵과의 호환성을 위해 만들어졌다.

```js
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// 어떤 고객(john, mary)은 여러 번 방문할 수 있다.
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// 중복을 허용하지 않는다.
alert( set.size ); // 3

for (let user of set) {
  alert(user.name); // // John, Pete, Mary 순으로 출력된다.
}
```