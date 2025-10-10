---
title: 루프와 반복
slug: Web/JavaScript/Guide/Loops_and_iteration
l10n:
  sourceCommit: fad67be4431d8e6c2a89ac880735233aa76c41d4
---

{{PreviousNext("Web/JavaScript/Guide/Control_flow_and_error_handling", "Web/JavaScript/Guide/Functions")}}

루프는 어떤 것을 반복적으로 시행할때 빠르고 간편한 방법을 제공합니다. 
[JavaScript Guide](/ko/docs/Web/JavaScript/Guide)의 이 항목은 
JavaScript 에서 사용이 가능한 서로 다른 여러가지 반복문을 소개합니다.

반복문을 게임의 컴퓨터화된 버전이라고 생각해 보세요. 누군가에게 한 방향으로
_X_만큼 가게 시키고 다른 방향으로 _Y_만큼 더 가게 한다고 생각해 보십시오. 
예를들어, "동쪽으로 5만큼 가세요"는 다음과 같이 반복문으로 표현 될 수 있습니다.

```js
for (let step = 0; step < 5; step++) {
  // step의 값이 0부터 4까지로, 5번 실행됩니다.
  console.log("Walking east one step");
}
```

반복문은 매우 다양한 종류가 있습니다. 하지만 반복문이 기본적으로 하는일은 모두 같습니다. 
반복문은 한 동작을 여러 번 반복합니다. 
(사실 0회 반복하는 것도 가능합니다.) 

여러 가지 반복문 구조는 반복의 시작점과 끝점을 결정하는 
서로 다른 방법을 제공합니다.
상황에 따라 어떤 종류의 반복문이 다른 반복문보다 더 적합한 경우도 있습니다.

JavaScript가 지원하는 반복문은 다음과 같습니다:

- [for 문](#for_문)
- [do...while 문](#do...while_문)
- [while 문](#while_문)
- [레이블 문](#레이블_문)
- [break 문](#break_문)
- [continue 문](#continue_문)
- [for...in 문](#for...in_문)
- [for...of 문](#for...of_문)

## `for` 문

{{jsxref("Statements/for", "for")}} 반복문은 지정한 조건이 거짓으로 평가될 때까지 반복합니다. JavaScript의 `for` 반복문은 JAVA와 C의 `for` 반복문과 비슷합니다.

`for` 문은 다음과 같습니다:

```js-nolint
    for ([초기문]; [조건문]; [증감문])
      실행문
```

for문이 실행될 때, 다음과 같이 실행됩니다.:

1. 초기화 구문인 `초기문`이 존재한다면 실행됩니다. 이 표현은 보통 한 개나 더 많은 반복문 카운터로 초기 설정이 됩니다. 그러나 복잡한 구문으로 표현 될 때도 있습니다. 또한 변수로 선언 되기도 합니다.
2. `조건문`은 조건을 검사합니다. 만약 `조건문`이 참이라면, 그 반복문은 실행됩니다. 그렇지 않다면 `for` 반복문은 종료됩니다. 만약 그 `조건문`이 생략된다면, 그 조건문은 참으로 추정됩니다.
3. `실행문`이 실행됩니다. 여러 개의 문장을 실행하려면, [블록문](/ko/web/javascript/reference/statements/block) (`{ }`)을 사용하여 해당 문장들을 묶어야 합니다.  
4. `증감문`이 존재한다면 실행됩니다.
5. 2번째 단계로 돌아갑니다.

### **예시**

아래 예제에서, 함수에는 스크롤 가능한 목록에서 선택된 옵션의 개수를 세는 `for` 문이 포함되어 있습니다.  
이 목록은 여러 항목을 선택할 수 있는 
[`<select>`](/en-US/docs/Web/HTML/Reference/Elements/select) 요소입니다.

#### html

```html
<form name="selectForm">
    <label for="musicTypes"
      >Choose some music types, then click the button below:</label
    >
    <select id="musicTypes" name="musicTypes" multiple="multiple">
      <option selected="selected">R&B</option>
      <option>Jazz</option>
      <option>Blues</option>
      <option>New Age</option>
      <option>Classical</option>
      <option>Opera</option>
    </select>
  <button id="btn" type="button">How many are selected?</button>
</form>
```

#### JavaScript

여기서 `for` 문은 변수 `i`를 선언하고 `0`으로 초기화합니다.  그 후, `i`가 `<select>` 요소의 옵션 개수보다 작은지 확인하고, 이어지는 `if` 문을 실행한 뒤,  각 반복이 끝날 때마다 `i`를 1씩 증가시킵니다.

```js
function countSelected(selectObject) {
  let numberSelected = 0;
  for (let i = 0; i < selectObject.options.length; i++) {
    if (selectObject.options[i].selected) {
      numberSelected++;
    }
  }
  return numberSelected;
}

const btn = document.getElementById("btn");

btn.addEventListener("click", () => {
  const musicTypes = document.selectForm.musicTypes;
  console.log(`You have selected ${countSelected(musicTypes)} option(s).`);
});
```

## `do...while` 문

{{jsxref("statements/do...while", "do...while")}} 문은 지정된 조건이 
거짓으로 평가될 때 까지 반복됩니다.

`do...while`문은 다음과 같습니다:

```js-nolint
    do
      실행문
    while (조건문);
```

`실행문`은 조건문을 확인하기 전에 
항상 한 번 실행됩니다. 
(많은 문장을 실행하기 위해선 { }를 써서 문장들을 묶어줍니다.)
 
만약 `조건`이 `참`이라면, 그 문장은 다시 실행됩니다. 
매 실행 마지막마다 조건문이 확인됩니다. 
만약 조건문이 `거짓`일 경우, 실행을 멈추고 
`do...while` 문 바로 아래에 있는 문장으로 넘어가게 합니다.

### **예시**

다음 예제에서, `do` 반복문은 최소 한 번 반복됩니다. 
그리고 `i` 가 `5`보다 작지 않을 때까지 계속 반복됩니다.

```js
let i = 0;
do {
  i += 1;
  console.log(i);
} while (i < 5);
```

## `while` 문

{{jsxref("Statements/while", "while")}} 문은 지정된 조건이 
`true`로 평가되는 동안 그 내부의 문장들을 실행합니다.  
`while` 문은 다음과 같은 형태를 가집니다:

```js-nolint
    while (조건문)
      실행문
```

만약 `조건문`이 `거짓`이 된다면,
그 반복문 안의 `실행문`은 실행을 멈추고 
반복문 바로 다음의 문장으로 넘어갑니다.

조건문은 반복문 안의 `실행문`이 실행되기 _전에_ 확인 됩니다. 
만약 조건문이 `참`으로 리턴된다면, `실행문`은 실행되고 
그 조건문은 다시 판별됩니다. 
만약 조건문이 `거짓`으로 리턴된다면, 
실행을 멈추고 `while`문 바로 다음의 문장으로 넘어가게 됩니다.

많은 문장들을 실행하기 위해선, (`{ }`)를 써서 
문장들을 묶어줍니다.

### **예시 1**

다음 `while` 반복문은 `n`이 `3`보다 작은 한, 
계속 반복됩니다.

```js
let n = 0;
let x = 0;
while (n < 3) {
  n++;
  x += n;
}
```

매 반복과 함께, `n`이 증가하고 `x`에 더해집니다. 
그러므로, `x`와 `n`은 
다음과 같은 값을 갖습니다.

- 첫번째 경과 후
  : `n` = 1 and `x` = 1
- 두번째 경과 후
  : `n` = 2 and `x` = 3
- 세번째 경과 후
  : `n` = 3 and `x` = 6

세번째 경과 후에, `n < 3` 은 더이상 `참`이 아니므로, 
반복문은 종결됩니다.

### **예시 2**

조건문은 항상 `거짓`이 될지라도 
무한 루프는 피해야 합니다. 
그렇지 않으면 그 반복문은 영원히 끝나지 않을 것입니다. 
아래의 `while` 문은 조건문이 절대 `거짓`이 될 수 없으므로 영원히 반복될 것입니다.

```js 나쁜 예제
// 무한 루프는 나쁩니다.
while (true) {
  console.log("Hello, world");
}
```

## 레이블 문

{{jsxref("Statements/label", "레이블")}}은 여러분이 프로그램에서 다른 곳으로 참조할 수 있도록 
식별자로 문을 제공합니다. 예를 들어, 여러분은 루프를 식별하기 위해 레이블을 사용하고,
프로그램이 루프를 방해하거나 실행을 계속할지 여부를 나타내기 위해 
`break`나 `continue` 문을 사용할 수 있습니다.

레이블 문의 구문은 다음과 같습니다:

```js-nolint
    label :
       statement
```

`레이블`의 값은 예약어가 아닌 어떤 JavaScript 식별자라도 사용할 수 있습니다.  
레이블로 지정한 `실행문`는 어떤 문장이라도 될 수 있습니다.  
레이블 문을 사용하는 예시는 아래의 `break`와 `continue` 예제에서 확인할 수 있습니다.

## `break` 문

{{jsxref("Statements/break", "break")}} 문은 반복문(`loop`)이나 `switch`문을 종료하거나,  
레이블이 지정된 문장과 함께 사용하여 해당 구문을 즉시 종료할 때 사용합니다.

- 레이블 없이 `break`문을 쓸 때: 가장 가까운 `while`, `do-while`,     `for`, 또는 `switch`문을 
  즉시 종료하고 
  다음 명령어로 넘어갑니다.
- `break`를 레이블 문에서 쓸 때 
  특정 레이블 문에서 끝납니다.

`break`문의 문법은 다음과 같습니다.

```js-nolint
break;
break label;
```

1. 첫 번째 형태의 구문은 가장 안쪽에 있는 반복문(`loop`)이나 `switch`문을 종료합니다.  
2. 두 번째 형태의 구문은 지정된 레이블이 붙은 문장을 종료합니다.

### 예시 1

다음 예제는 배열의 요소를 순회하면서,
값이 `theValue`인 요소의 인덱스를 찾을 때까지 반복합니다.

```js
for (let i = 0; i < a.length; i++) {
  if (a[i] === theValue) {
    break;
  }
}
```

### 예시 2: 레이블로 빠져나가기 (Breaking to a label)

```js
let x = 0;
let z = 0;
labelCancelLoops: while (true) {
  console.log("Outer loops:", x);
  x += 1;
  z = 1;
  while (true) {
    console.log("Inner loops:", z);
    z += 1;
    if (z === 10 && x === 10) {
      break labelCancelLoops;
    } else if (z === 10) {
      break;
    }
  }
}
```

## continue 문

{{jsxref("Statements/continue", "continue")}}문은 
`while`, `do-while`, `for`, `레이블` 문을 
다시 시작하기 위해 사용될 수 있습니다.

- 레이블없이 `continue`를 사용하는 경우, 
그것은 가장 안쪽의 `while`, `do-while`, `for` 문을 둘러싼
현재 반복을 종료하고, 
다음 반복으로 루프의 실행을 계속합니다. 
`break`문과 달리, 
`continue` 문은 전체 루프의 실행을 종료하지 않습니다. 
`while` 루프에서 그것은 다시 조건으로 이동합니다. `for` 루프에서 그것은 `증가 표현`으로 이동합니다.
- 레이블과 함께 `continue`를 사용하는 경우,
 `continue`는 그 레이블로 식별되는 루프 문에 적용됩니다.

`continue` 문의 구문은 다음과 같습니다:

```js-nolint
continue;
continue label;
```

### 예시1

다음의 예는 `i` 값이 `3`일 때 실행하는 `continue` 문과 함께
`while` 루프를 보여줍니다.
 따라서, `n`은 값 `1`, `3`, `7`, 
 `12`를 취합니다.

```js
let i = 0;
let n = 0;
while (i < 5) {
  i++;
  if (i === 3) {
    continue;
  }
  n += i;
  console.log(n);
}
// Logs:
// 1 3 7 12
```

`continue;` 문을 주석 처리하면, 반복문이 끝까지 실행되어 `1, 3, 6, 10, 15`가 출력됩니다.

### 예시2

`checkiandJ` 레이블 문은 `checkJ` 레이블 문을 포함합니다. 
`continue`가 발생하는 경우, 
프로그램은 `checkJ`의 현재 반복을 종료하고, 다음 반복을 시작합니다. 
그 조건이 `false`를 반환 할 때까지 `continue`가 발생할 때마다, 
`checkJ`는 반복합니다. `false`가 반환될 때,
`checkiandJ` 문의 나머지 부분은 완료되고, 
그 조건이 `false`를 반환 할 때까지 `checkiandJ`는 반복합니다. 
`false`가 반환될 때,
이 프로그램은 다음 `checkiandJ` 문에서 계속됩니다.

`continue`가 `checkIandJ`의 레이블을 가지고 있다면, 
프로그램은 `checkIandJ` 문 상단에서 계속될 것입니다.

```js
let i = 0;
let j = 10;
checkIandJ: while (i < 4) {
  console.log(i);
  i += 1;
  checkJ: while (j > 4) {
    console.log(j);
    j -= 1;
    if (j % 2 === 0) {
      continue;
    }
    console.log(j, "is odd.");
  }
  console.log("i =", i);
  console.log("j =", j);
}
```

## `for...in` 문

 {{jsxref("Statements/for...in", "for...in")}}문은 객체의 열거 속성을 통해 지정된 변수를 반복합니다. 
 각각의 고유한 속성에 대해, JavaScript는 지정된 문을 실행합니다. 
 `for...in` 문은 다음과 같습니다:

```js-nolint
for (variable in object) {
  statements
}
```

### **예시**

다음 함수는 객체와 객체의 이름을 함수의 인수로 취합니다.
그런 다음 모든 객체의 속성을 반복하고 
속성 이름과 값을 나열하는 문자열을 반환합니다.

```js
function dumpProps(obj, objName) {
  let result = "";
  for (const i in obj) {
    result += `${objName}.${i} = ${obj[i]}<br>`;
  }
  result += "<hr>";
  return result;
}
```

속성 `make`와 `model`을 가진 객체 `car`의 경우, `결과`는 다음과 같습니다:

```plain
car.make = Ford
car.model = Mustang
```

### **배열**

{{jsxref("배열")}} 요소를 반복하는 방법으로 이를 사용하도록 유도될 수 있지만, 
`for...in` 문은 숫자 인덱스에 추가하여 
사용자 정의 속성의 이름을 반환합니다. 

따라서 만약 여러분이 사용자 정의 속성 또는 메서드를 추가하는 등 Array 객체를 수정한다면, 
배열 요소 이외에도 사용자 정의 속성을 통해 `for...in` 문을 반복하기 때문에, 
배열을 통해 반복할 때 숫자 인덱스와 
통상적인 {{jsxref("Statements/for", "for")}} 루프를 사용하는 것이 좋습니다.

## for...of 문

{{jsxref("Statements/for...of", "for...of")}} 문은  
[반복 가능한 객체](/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)  
(예: {{jsxref("Array")}}, {{jsxref("Map")}}, {{jsxref("Set")}},  {{jsxref("Functions/arguments", "arguments")}} 객체 등)을 순회하는 반복문을 생성합니다.  
각 요소의 값을 대상으로 실행할 문장을 수행하며, 
필요할 경우 사용자 정의 반복 훅을 호출합니다.

```js-nolint
for (variable of iterable)
  statement
```

다음 예제는 `for...of` 루프와 {{jsxref("Statements/for...in", "for...in")}} 루프의 차이를 보여줍니다.  
`for...in`은 속성 이름을 반복하는 반면,  
`for...of`는 속성 값을 반복합니다.

```js
const arr = [3, 5, 7];
arr.foo = "hello";

for (const i in arr) {
  console.log(i);
}
// "0" "1" "2" "foo"

for (const i of arr) {
  console.log(i);
}
// Logs: 3 5 7
```

`for...of`와 `for...in` 문은 [구조 분해 할당](/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring)과 함께 사용할 수도 있습니다. 예를 들어, {{jsxref("Object.entries()")}}를 사용하면 객체의 키와 값을 동시에 반복할 수 있습니다.

```js
const obj = { foo: 1, bar: 2 };

for (const [key, val] of Object.entries(obj)) {
  console.log(key, val);
}
// "foo" 1
// "bar" 2
```

{{PreviousNext("Web/JavaScript/Guide/Control_flow_and_error_handling", "Web/JavaScript/Guide/Functions")}}
