# 의미 있는 이름

## 의도를 분명히 밝혀라

- 따로 주석이 필요하다면 의도를 분명히 드러내지 못했다는 말이다.

### X

```js
// js
let d; // 경과 시간(단위: 날짜)
```

```ts
// ts
let d: number; // 경과 시간(단위: 날짜)
```

### O

```js
// js
let elapsedTimeInDays;
let daysSinceCreation;
let daysSinceModification;
let fileAgeInDays;
```

```ts
// ts
let elapsedTimeInDays: number;
let daysSinceCreation: number;
let daysSinceModification: number;
let fileAgeInDays: number;
```

- 코드의 단순성이 아니라 코드의 함축성. 코드 맥락이 코드 자체에 명시적으로 드러나게
- 지뢰찾기 게임을 가정, 값4는 깃발이 꽂힌 상태

### X

```js
// js
function getThem() {
  const list1 = [];
  for (x of theList) {
    if (x[0] == 4) {
      list1.push(x);
    }
  }
  return list1;
}
```

```ts
// ts
function getThem() {
  const list1: number[] = [];
  for (x as number[] of theList as number[][]) {
    if (x[0] == 4) {
      list1.push(x);
    }
  }
  return list1;
}
```

### O

```js
// js
function getFlaggedCells() {
  const flaggedCells = [];
  for (cell of gameBoard) {
    if (cell[STATUS_VALUE] == FLAGGED) {
      flaggedCells.push(cell);
    }
  }
  return flaggedCells;
}
```

```ts
// ts
function getFlaggedCells() {
  const flaggedCells: number[] = [];
  for (cell as number[] of gameBoard as number[][]) {
    if (cell[STATUS_VALUE] == FLAGGED) {
      flaggedCells.push(cell);
    }
  }
  return flaggedCells;
}
```

### O

```js
// js
function getFlaggedCells() {
  const flaggedCells = [];
  for (cell of gameBoard) {
    if (cell.isFlagged()) {
      flaggedCells.push(cell);
    }
  }
  return flaggedCells;
}
```

```ts
// ts
function getFlaggedCells() {
  const flaggedCells: Cell[] = [];
  for (cell as Cell[] of gameBoard as Cell[][]) {
    if (cell.isFlagged()) {
      flaggedCells.push(cell);
    }
  }
  return flaggedCells;
}
```

## 그릇된 정보를 피하라

- 예를 들어 계정을 담는 컨테이너가 실제 List(Array, Map)가 아니라면 프로그래머에게 그릇된 정보를 제공하는 셈
- 실제 컨테이너가 List(Array, Map)인 경우라도 컨테이너 유형을 이름에 넣지 않는 편이 바람직하다.

### X

```
accountList
```

### O

```
accountGroup, bunchOfAccounts, accounts
```

## 의미 있게 구분하라

- 컴파일러를 통과할지라도 연속된 숫자를 덧붙이거나 불용어noise word를 추가하는 방식은 적절하지 못하다. 이름이 달라야 한다면 의미도 달라져야 한다.

### X

```js
// js
function copyChars(a1, a2) {
  for (let i = 0; i < a1.length; i++) {
    a2[i] = a1[i];
  }
}
```

```ts
// ts
function copyChars(a1: string[], a2: string[]) {
  for (let i = 0; i < a1.length; i++) {
    a2[i] = a1[i];
  }
}
```

### O

```js
// js
function copyChars(source, destination) {
  for (let i = 0; i < source.length; i++) {
    destination[i] = source[i];
  }
}
```

```ts
// ts
function copyChars(source: string[], destination: string[]) {
  for (let i = 0; i < source.length; i++) {
    destination[i] = source[i];
  }
}
```

## 발음하기 쉬운 이름을 사용하라

- 발음하기 어려운 이름은 토론하기도 어렵다. 바보처럼 들리기 십상이다.
- genymdhms: generate date, year, month, day, hour, minute, second, “젠 와이 엠 디 에이취 엠 에스”

### X

```js
// js
function DtaRcrd102() {
  let genymdhms;
  let modymdhms;
  const pszqint = "102";
}
```

```ts
// ts
function DtaRcrd102() {
  let genymdhms: Date;
  let modymdhms: Date;
  const pszqint = "102";
}
```

### O

```js
// js
function Customer() {
  let generationTimestamp;
  let modificationTimestamp;
  const recordId = "102";
}
```

```ts
// ts
function Customer() {
  let generationTimestamp: Date;
  let modificationTimestamp: Date;
  const recordId = "102";
}
```
