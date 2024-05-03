# .d.ts
.d.ts 는 javascript 파일을 typescript파일로 변환해서 사용가능하게 해준다.

우선, Node.js 프로젝트를 빠르게 생성한다.
```javascript
npm init -y
```
​
이제 tsconfig.json을 생성하여 TypeScript 프로젝트로 변환한다. 
```javascript
tsc --init
```
​
tsconfig.json을 열어서 아래의 옵션을 주석 해제하여 true로 설정한다.
```javascript
"allowJs": true // TypeScript 프로젝트에 JavaScript 파일 허용 여부
"checkJs": true // JavaScript 파일 타입 체크 여부
```
​
TypeScript에서 사용하고 싶은 커스텀 JavaScript 라이브러리(test.js)를 만든다.
```javascript
/**
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
export function add(a, b) { 
  return a + b;
}
```
​
위의 주석문은 JSDoc이라고 한다.
JSDoc은 API의 시그니처 (인자, 리턴 타입)를 설명하는 HTML 문서 생성기이다.
JSDoc으로 자바스크립트 소스코드에 타입 힌트를 제공할 수 있다.
이제, JSDoc으로 타입 힌트가 제공된 test.js의 .d.ts 파일을 만든다. 다음의 명령어를 복사 + 붙여넣기를 해서 터미널에서 실행해준다.
```javascript
npx tsc test.js --declaration --allowJs --emitDeclarationOnly --outDir types
```
​
types/test.d.ts 파일을 확인하면 다음과 같이 생성이 되어 있다.
```javascript
/**
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
export function add(a: number, b: number): number;
```
​
test.js 파일을 참조할 foo.ts 파일을 새로 만든다.
```javascript
import { add } from "./test";
console.log(add(1, 2));
```
​
이제 foo.ts 파일을 실행시켜 보자
```javascript
npx ts-node foo.ts
```