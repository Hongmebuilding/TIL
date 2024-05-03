# const, let, readonly
|  let |const   |read only   |
| ------------ | ------------ | ------------ |
|변성   |  불변성 |  불변성 |

##### readonly 사용사례
```javascript
class Person {
  readonly name: string;
  readonly age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

const person = new Person('Spartan', 30);

console.log(person.name);  // 출력: 'Spartan'
console.log(person.age);   // 출력: 30

person.name = 'Jane';  // 에러: 'name'은 readonly 속성이므로 다시 할당할 수 없다.
person.age = 25;       // 에러: 'age'은 readonly 속성이므로 다시 할당할 수 없다.
```
|any   |unknown   |union   |
| ------------ | ------------ | ------------ |
|자바의 Object  |any와 비슷하나 Type Assertion이라는 속성이 있음   |여러 타입 중 하나를 가질 수 있는 변수를 선언할 때 사용   |

##### unknown 사용사례
```javascript
let unknownValue: unknown = '나는 문자열이지롱!';

let stringValue: string;
stringValue = unknownValue; // 에러 발생! unknownValue가 string임이 보장이 안되기 때문!
stringValue = unknownValue as string; // Type Assertion(타입 단언)
```

```javascript
let unknownValue: unknown = '나는 문자열이지롱!';
let stringValue: string;

if (typeof unknownValue === 'string') {
  stringValue = unknownValue;
  console.log('unknownValue는 문자열이네요~');
} else {
  console.log('unknownValue는 문자열이 아니었습니다~');
}
```

`typeof` 키워드를 이용하여 타입 체크를 미리한 후 unknown 타입의 변수를 string 타입의 변수에 할당할 수 있다.

