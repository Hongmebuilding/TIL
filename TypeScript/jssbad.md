# 참고 문헌 - TeamSparta
# JavaScript의 약점
 ## 배경
 - 페이지에 동적인 효과를 주기 위해 만들어진 스크립트 언어
 - JavaScript의 성능을 높이고자 하는 니즈가 있었고 구글에서 V8 엔진이라는 것을 만들어서 세상에 공개했다
 - 이것에 그치지 않고 V8 엔진의 우수한 성능을 기반으로 Node.js라는 플랫폼이 나와서 JavaScript로도 백엔드를 작성할 수 있게 되었다
> Node.js의 잠재적 위험성
 예외 처리가 제대로 되지 않은 백엔드의 단순한 에러 하나로 인해 서버가 다운될 수 있다(503)
 
## 프로그램을 실행 때 에러를 알게된다
1. 실행 시간에 결정되는 변수 타입
 -JavaScript는 변수의 타입이 실행 시간에 결정된다
 -변수에 잘못된 타입의 값이 할당되어 발생한 오류를 찾기 위해서는 실행 시간에 변수의 값과 타입을 모두 확인해야 하는 번거로움이 있다
2. 약한 타입 체크
 -`let a = 1; a = “Hello”;` 이것이 가능!
3. 컴파일러가 실수를 못잡음
 ```javascript
const obj = { apple: 11.5, banana: 47.1 };
const result = obj.apple * obj.banananana;
console.log(result) // NaN
```
