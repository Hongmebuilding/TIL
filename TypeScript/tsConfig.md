# tsconfig.json 해부하기
TypeScript 프로젝트의 설정을 최적화 할 수 있게 한다.
`tsc --init` 명령을 실행하면 생성된다.
↘[옵션 메뉴얼](https://www.typescriptlang.org/ko/tsconfig)

### ☑️ compilerOptions - module 옵션

- TypeScript 파일을 컴파일한 후 생성되는 JavaScript 모듈의 형식을 지정한다
- 모듈을 가져오고 내보내는 방식을 결정하는 옵션이라고 생각하면 된다
- **target 옵션과는 서로 독립적인 관계**니 프로젝트의 요구사항에 따라 옵션을 설정하시면 된다

### ☑️ compilerOptions - outDir 옵션

- 컴파일된 JavaScript 파일이 저장될 출력 디렉터리를 지정한다
- 예를 들어, `"outDir": "dist"`로 설정하면 컴파일된 파일들이 `dist` 폴더에 저장
- `compilerOptions - strict` 옵션
    - 엄격한 타입 검사 옵션을 모두 활성화하는 옵션이다
    - TypeScript 컴파일러가 보다 엄격한 타입 검사를 수행해 코드의 실수를 미리 찾아낼 수 있다
    - 해당 옵션을 true로 설정하면 아래의 옵션들이 자동으로 true로 설정이 된다
        - `strictNullChecks`
            - 잠재적으로 null(undefined)이 될 수 있는 값들에 대해서 엄격하게 확인하는 옵션
        - `strictFunctionTypes`
        - `strictBindCallApply`
        - `strictPropertyInitialization`
        - `noImplicitAny`
            - 함수의 인자 또는 변수의 타입이 명시적으로 선언되지 않은 경우에 컴파일러가 자동으로 `any`타입을 부여하지 않도록 한다.
            - 이 옵션을 활성화하면 개발자가 누락된 타입 선언을 확인하고 명시적으로 타입을 선언할 수 있다!
        - `noImplicitThis`
        - `alwaysStrict`
    - 당연하게도, **해당 옵션은 꼭 true로 설정하는 것을 권장.**

### ☑️ compilerOptions - sourceMap 옵션

- 컴파일된 JavaScript 파일에 대한 소스 맵을 생성하는 옵션
- 소스 맵을 사용하면 실행 중에 에러가 발생했을 때 원래 TypeScript 소스 코드의 위치를 확인할 수 있다.
- 코드 디버깅에 매우 큰 도움이 되기 때문에 **개발 환경**에서는 **꼭 true로 설정하시는 것을 권장.**
    - 프로덕션 환경에서는 용량이나 성능상의 이유로 sourceMap을 사용하지 않는 것이 나을 수 있다

### ☑️ include , exclude 옵션

- tsc가 컴파일을 할 때 포함하거나 제외할 파일이나 디렉터리를 지정하는 옵션
- “include": ["src/**/*"]
    - src 디렉토리 밑의 친구들을 컴파일 하겠다는 의미이다.
- "exclude": ["node_modules", "dist"]
    - node_modules, dist 디렉토리 밑의 친구들은 컴파일 대상에서 제외하겠다는 의미이다.