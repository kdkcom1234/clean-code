# 의미 있는 이름

## 의도를 분명히 밝혀라

- 따로 주석이 필요하다면 의도를 분명히 드러내지 못했다는 말이다.

### X

```js
let d; // 경과 시간(단위: 날짜)
```

### O

```js
let elapsedTimeInDays;
let daysSinceCreation;
let daysSinceModification;
let fileAgeInDays;
```

- 코드의 단순성이 아니라 코드의 함축성. 코드 맥락이 코드 자체에 명시적으로 드러나게
- 지뢰찾기 게임을 가정, 값4는 깃발이 꽂힌 상태

### X

```js
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

### O

```js
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

### O

```js
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
function copyChars(a1, a2) {
  for (let i = 0; i < a1.length; i++) {
    a2[i] = a1[i];
  }
}
```

### O

```js
function copyChars(source, destination) {
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
function DtaRcrd102() {
  let genymdhms;
  let modymdhms;
  const pszqint = "102";

  return { genymdhms, modymdhms, pszqint };
}
```

### O

```js
function Customer() {
  let generationTimestamp;
  let modificationTimestamp;
  const recordId = "102";

  return { generationTimestamp, modificationTimestamp, recordId };
}
```

## 검색하기 쉬운 이름을 사용하라

- 긴 이름이 짧은 이름보다 좋다. 검색하기 쉬운 이름이 상수보다 좋다.
- 간단한 메서드에서 로컬 변수만 한 문자를 사용한다.

### X

```js
for (let j = 0; j < 34; j++) {
  s += (t[j] * 4) / 5;
}
```

### O

```js
let realDaysPerIdealDay = 4;
const WORK_DAYS_PER_WEEK = 5;
let sum = 0;
for (let j = 0; j < NUMBER_OF_TASKS; j++) {
  let realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
  let realTaskWeeks = realTaskDays / WORK_DAYS_PER_WEEK;
  sum += realTaskWeeks;
}
```

## 인코딩을 피하라

[헝가리식 표기법]

- 자바크로그래머는 변수 이름에 타입을 인코딩할 필요가 없다. 컴파일러나 IDE에서 강제함, 타입변환의 불편함 발생.
- (의견) 타입스크립트에서는 쓸 필요가 없으나 자바스크립트에서는 쓰는 것도 괜찮다고 생각함.

```js
// js
let phoneString;
```

```ts
// ts
// 타입이 바뀌어도 이름은 바뀌지 않는다!
let phoneString: string;
let phoneString: PhoneNumber;
```

[멤버 변수 접두어]

- 이제는 멤버 변수에 m\_이라는 접두어를 붙일 필요도 없다
- 멤버 변수를 다른 색상으로 표 시하거나 눈에 띄게 보여주는 IDE를 사용해야 마땅하다.

### X

```js
function Part() {
  let m_dsc; // 설명 문자열
  function setName(name) {
    this.m_dsc = name;
  }

  return { m_dsc, setName };
}
```

### O

```js
function Part() {
  let description;
  function setDescription(description) {
    this.description = description;
  }

  return { description, setDescription };
}
```

[인터페이스 클래스와 구현 클래스]

- 개인적으로 인터페이스 이름은 접두어를 붙이지 않는 편이 좋다고 생각한다.
- 인터페이스 클래스 이름과 구현 클래스 이름 중 하나를 인코딩해야 한다면 구현 클래스 이름을 택하겠다
  - 코멘트: 인터페이스는 두 가지 관점으로 사용함
    1. 형식의 강제화: 인터페이스 정의한 메서드를 구현하지 않으면 오류 발생
    2. 다형성: 구현클래스를 교체하여 사용가능함.
  - 예를 들어 자바에서는 인터페이스 타입은 변수에 구현 클래스를 대입할 수 있음.
  - 또한 인터페이스 타입의 변수에서 메서드를 호출하면 구현 클래스의 메서드가 호출되는 구조(징검다리역할)

```java
// java
ShapeFactory factory = new ShapeFactoryImp();
factory.createShape();  // ShapeFactoryImp의 메서드가 호출됨
factory = new ShapeFactoryImpV2();
factory.createShape();  // ShapeFactoryImpV2의 메서드가 호출됨
```

- C#에서는 주로 I를 인터페이스에 붙임, 타입스크립트에서는 컨벤션은 없어보임

```cs
// C#
// https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/keywords/interface
// C#도 자바와 비슷하게 사용가능하나 MSDN에서는 주로 인터페이스에 I를 붙임
interface ISampleInterface
{
  void SampleMethod();
}
class ImplementationClass : ISampleInterface
{

  void ISampleInterface.SampleMethod(){}

  static void Main()
  {
      // Declare an interface instance.
      ISampleInterface obj = new ImplementationClass();

      // Call the member.
      obj.SampleMethod();
  }
}
```

```ts
// TS
// 클래스에 메서드 미선언시에 컴파일 에러 발생
// https://www.typescriptlang.org/docs/handbook/2/classes.html#class-heritage
interface Pingable {
  ping(): void;
}

class Sonar implements Pingable {
  ping() {
    console.log("ping!");
  }
}

class Ball implements Pingable {
  // Class 'Ball' incorrectly implements interface 'Pingable'.
  //   Property 'ping' is missing in type 'Ball' but required in type 'Pingable'.
  pong() {
    console.log("pong!");
  }
}

interface ClockInterface {
  currentTime: Date;
  setTime(d: Date): void;
}

class Clock implements ClockInterface {
  currentTime: Date = new Date();
  setTime(d: Date) {
    this.currentTime = d;
  }
  constructor(h: number, m: number) {}
}

// 자바와 동일하게 인터페이스 타입의 변수에 구현 클래스 타입 인스턴스를 대입 가능함
// 인터페이스 타입의 변수에 속성을 읽으면 구현 클래스의 인스턴스의 속성이 읽어짐
interface A {
  x: number;
  y?: number;
}
class C implements A {
  x = 0;
}

let a: A = new C();
console.log(a.x, a.y);
```

- 타입스크립트에서도 하나로 통일하는게 좋아보임.
- 컴포넌트명(함수명, 클래스명)과 인터페이스명이 겹치는 경우가 있어 [이름][용도], I[이름], I[이름][용도] 이런형태가 어떨런지

```tsx
// [이름][용도]
interface HeaderProps {
  title: string;
}
function Header({ title }: HeaderProps) {
  return <div>{title}</div>;
}

// I[이름]
interface IHeader {
  title: string;
}
function Header({ title }: IHeader) {
  return <div>{title}</div>;
}

// 현재 쓰는 방법
// I[이름][용도]
interface IHeaderProps {
  title: string;
}
function Header({ title }: IHeaderProps) {
  return <div>{title}</div>;
}

// I[이름][용도]
interface IProfileData {
  userName: string;
}
function Profile() {
  let profileData: IProfileData = { userName: "고대근" };
}
```

## 자신의 기억력을 자랑하지 마라

- 독자가 코드를 읽으면서 변수 이름을 자신이 아는 이름으로 변환해야 한다면 그 변수 이름은 바람직하지 못하다
- r이라는 변수가 호스트와 프로토콜을 제외한 소문자 URL이라는 사실을 언제나 기억한다면 확실히 똑똑한 사람이다.

## 클래스 이름

- 클래스 이름과 객체 이름은 명사나 명사구가 적합하다. 동사는 사용하지 않는다.
- 덧: 일반적인 명사는 피하라는 것 같음

### X

```
Manager, Processor, Data, Info
```

### O

```
Customer, WikiPage, Account, AddressParser
```

## 메서드 이름

- 메서드 이름은 동사나 동사구가 적합하다.

```
postPayment, deletePage, save
```

- 접근자Accessor, 변경자Mutator, 조건자Predicate는 javabean 표준4에 따 라 값 앞에 get, set, is를 붙인다.

```js
const name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted()) {
}
```

- 생성자 오버로딩, 정적 팩터리 메서드를 사용하는 것이 좋다.(자바 스타일)
- 참고: https://tecoble.techcourse.co.kr/post/2020-05-26-static-factory-method/

```java
// java
// O
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
// X
Complex fulcrumPoint = new Complex(23.0);
```

- 타입스크립트 생성자 오버로딩 참고

```ts
interface IBox {
  x: number;
  y: number;
  height: number;
  width: number;
}

class Box {
  public x: number;
  public y: number;
  public height: number;
  public width: number;

  constructor(obj?: IBox) {
    this.x = obj?.x ?? 0;
    this.y = obj?.y ?? 0;
    this.height = obj?.height ?? 0;
    this.width = obj?.width ?? 0;
  }
}
```

```ts
interface IBox {
  x: number;
  y: number;
  height: number;
  width: number;
}

class Box {
  public x: number;
  public y: number;
  public height: number;
  public width: number;

  constructor();
  constructor(obj: IBox);
  constructor(obj?: IBox) {
    this.x = obj?.x ?? 0;
    this.y = obj?.y ?? 0;
    this.height = obj?.height ?? 0;
    this.width = obj?.width ?? 0;
  }
}
```
