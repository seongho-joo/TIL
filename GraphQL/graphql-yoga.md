# graphql-yoga

- `grpahql-yoga`는 간단한 개발환경 세팅과 퍼포먼스, 개발 경험에 초점을 맞춘 GraphQL 서버
- `express`와 `graphQL server`인 `apollo-server`를 기반을 만들어짐

## graphql-yoga intall
```
$ yarn init
$ yarn add grapql-yoga
```

## graphQL의 장점
- `over-fetching`과 `undef-fetcing`을 해결 할 수 있음.
  - `over-fetching`
    -  API를 호출 시 필요보다 많은 데이터(사용하지 않을)를 가져오는 것을 말함
  - `under-fetching`
    - 하나의 endpoint로의 요청으로는 충분한 데이터를 받지 못하는 것을 말함

## Node.js에서 import 구문 사용
`$ yarn add babel-node --dev`