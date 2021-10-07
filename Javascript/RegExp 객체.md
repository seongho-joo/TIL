# RegExp

`RegExp`객체는 리터럴 표기법과 생성자로서 생성할 수 있음.
- **리터럴 표기볍**의 매개변수는 `/`으로 감싸고 `'`를 사용하지 않음
- **생성자 함수**의 매개변수는 `/`으로 감싸지 않으나  `'`를 사용함

```js
new RegExp(/ab+c/, 'i') // 리터럴
new RegExp('ab+c', 'i') // 생성자
```
- 사용 예
```js
for (let i in word) {
    const regex = new RegExp(word[i], 'g');
    s = s.replace(regex, i);
  }
```
