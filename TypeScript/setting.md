# 개발환경 구축
1. 우선은 Node.js가 안깔려 있다면 Node.js를 깔아야 한다. npm이라는 Node.js 기반 패키지 매니저를 통해서 TypeScript를 설치할 수 있다.
2. 설치 완료시 cmd 에 `nvm` 을 쳐서 확인한다.
3. nvm install [설치할 노드 버전]명령을 실행하여 Node.js를 설치한다.
4. nvm use [설치한 노드 버전] 명령을 실행하여 Node.js를 활성화한다.
5. `npm -v`를 쳐서 npm이 설치되었는지 확인한다.
6.  `npm install typescript -g` 를 실행하여 TypeScript를 글로벌하게 설치한다.
7.  `tsc` 를 쳐서 typescript가 제대로 설치가 된 것인지 확인한다.