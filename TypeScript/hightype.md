## enum vs. object literal
#### enum 
```javascript
enum UserRole {
  ADMIN = "ADMIN",
  EDITOR = "EDITOR",
  USER = "USER",
}
```
#### object literal
```javascript
const obj = {
  a: [1,2,3],
  b: 'b',
  c: 4
}
```
---
### 어떨 때 enum을 쓰고 어떨 때 object literal을 쓸까?
- enum 은 간단한 상수 값일 경우에 쓴다. 너무 자주 변하면 오히려 안 쓰는 것이 좋다.
- 객체 리터럴은 멤버의 값이나 데이터 타입을 맘대로 변경 가능

## 유틸리티 타입 훑어보기
기본 타입을 변형하거나 조작하기 위한 몇 가지 유틸리티 타입을 제공한다. 
- ### `Partial<T>`
타입 T의 모든 속성을 선택저긍로 만든다.
기존 타입의 일부만 제공해도 생성 가능
#### 활용사례
```javascript
interface Person {
  name: string;
  age: number;
}

const updatePerson = (person: Person, fields: Partial<Person>): Person => {
  return { ...person, ...fields };
};

const person: Person = { name: "Spartan", age: 30 };
const changedPerson = updatePerson(person, { age: 31 });
```
- ### `Required<T>`
not null 허용 하지 않을 때 사용
#### 활용사례
```javascript
interface Person {
  name: string;
  age: number;
  address?: string; // 속성 명 뒤에 붙는 ?가 뭘까요
}
  
  type RequiredPerson = Required<Person>;
```

- ### `Readonly<T>`
읽기 전용으로 만듦

- ### `Pick<T>`
`Pick<T, K>` 유틸리티 타입은 타입 T에서 K 속성들만 선택하여 새로운 타입을 만듦

```javascript
interface Person {
  name: string;
  age: number;
  address: string;
}

type SubsetPerson = Pick<Person, "name" | "age">;

const person: SubsetPerson = { name: "Spartan", age: 30 };
```
- ### `Omit<T>`
`Omit<T, K>` 유틸리티 타입은 타입 T에서 K 속성들만 제외한 새로운 타입을 만듦
`Pick<T, K>` 유틸리티 타입과는 반대의 동작
```javascript
interface Person {
  name: string;
  age: number;
  address: string;
}

type SubsetPerson = Omit<Person, "address">;

const person: SubsetPerson = { name: "Alice", age: 30 };
```
[utility reference](https://www.typescriptlang.org/ko/docs/handbook/utility-types.html)

