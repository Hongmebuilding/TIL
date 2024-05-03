# mini project
## 계산기 만들기
### 세팅
```javascript
npm init -y
```
```javascript
tsc --init --rootDir ./src --outDir ./dist --esModuleInterop --module commonjs --strict true --allowJS true --checkJS true
```
package.json의 scripts항목을 다음과 같이 변경
```javascript
"scripts": {
    "start": "tsc && node ./dist/index.js",
    "build": "tsc --build",
    "clean": "tsc --build --clean"
},
```
이제 현재 경로에서 src 디렉토리를 만들어 준다.
vsc 에서 현재 디렉토리 위치를 기반으로 편집기를 열어서 코딩 준비를 하기 위해 아래와 같이 입력한다.
```javascript
code .
```

------------

### 코딩
scr 폴더 안에 index.ts 라는 파일을 만들고 아래와 같은 함수를 만들자
```javascript
function assignGrade(average: number): string { ... }
```
> 조건
평균이 90점 이상이면 “A”, 80점 이상이면 “B”, 70점 이상이면 “C”, 60점 이상이면 “D”, 그 이하면 “F”를 주는 로직

<details>
  <summary>답안</summary>
  function assignGrade(average: number): string {
    if(average >= 90) return "A"
    else if(average >= 80) return "B"
    else if(average >= 70) return "C"
    else if(average >= 60) return "D"
    else return "F"
}
</details>
<br>

Student interface를 만들어 준다.
```javascript
interface Student {
  name: string;
  age: number;
  scores: {
    korean: number;
		math: number;
		society: number;
    science: number;
    english: number;
  };
}
```
> Student라는 타입의 객체를 받아서 평균을 계산하는 calculateAverage라는 함수를 만들자
```javascript
function calculateAverage(student: Student): number { ... }
```

<details>
  <summary>답안</summary>
  function calculateAverage(student: Student): number { 
    return student.scores.english + student.scores.korean + student.scores.math + student.scores.science + student.scores.society / Object.keys(student.scores).length; 
 }
</details>
<br>

> 학생을 만드는 함수를 만들어보자

<details>
  <summary>답안</summary>
  function createStudent(name: string, age: number, korean: number, math: number, society: number, science: number, english: number): Student {
    return {
      name,
      age,
      scores: {
        korean,
        math,
        society,
        science,
        english,
      },
    };
  }
</details>
<br>

> 성적을 출력하는 함수를 만들어보자

<details>
  <summary>답안</summary>
  function printResult(student: Student): void {
    let average = calculateAverage(student);
    let grade = assignGrade(average);
    console.log(`${student.name} (${student.age}세) - 평균: ${average.toFixed(2)}, 학점: ${grade}`);
}
</details>
<br>

이제 main 함수를 만들고 main 함수를 호출해보자
```javascript
function main(): void {
	const spartan = createStudent('Spartan', 30, 95, 89, 76, 90, 97);
	printResult(spartan);
}

main(); // main 함수를 호출
```
---
### 실행
해당 명령어로 프로젝트를 빌드한다.
```javascript
npm run build
```
그런 다음 아래를 입력하고 실행한다.
```javascript
npm run start
```