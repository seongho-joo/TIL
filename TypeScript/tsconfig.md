# tsconfig 옵션

## `noImplictAny`
- 변수들이 미리 정의된 타입을 가져야 하는지를 제어하는 옵션
- `noImplictAny`가 비활성화되었을 경우 타입스크립트 컴파일러는 타입을 any로 추론

```ts
function add(x, y) {
	return x + y
}
```

- `noImplictAny`가 활성화되었을 경우 타입을 반드시 명시해줘야 함

```ts
function add(x: number, y: number) {
	return x + y
}
```

## `strictNullChecks`
- `null`과 `undefined`가 모든 타입에서 허용되는지 확인하는 옵션
- `strictNullChecks`가 활성화되었을 때  `null`과 `undefined`  할당 불가능

```ts
const x: number | null = null
const y: number | undefined = undefined
```

- `strictNullChecks`가 비활성화되었을 때  `null`과 `undefined`  할당 가능 

```ts
const x: number = null
const y: number = undefined
```
