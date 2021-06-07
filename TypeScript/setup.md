# Typescript Setup

## typescript 설치
```
$ yarn add typescript
 or 
$ npm install typescript
```
## `tsconfig.json` 자동 생성 명령어
- global로 설치했을 경우 
  - `$ tsc --init`  
- local로 설치했을 경우
  - `$ npx tsc --init`

- `tsconfig.json`
```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true
  }
}
```
  - **target** : 컴파일된 코드가 어떤 환경에서 실행될지 정의
  - **module** : 컴파일된 코드가 어떤 모듈 시스템을 사용할지 정의
  - **strcit** : 모든 타입 체킹 옵션을 활성화할지 정의
  - **esModuleInterop** : `commonjs` 모듈 형태로 이루어진 파일을 es2015 모듈 형태로 불러올 수 있게 함