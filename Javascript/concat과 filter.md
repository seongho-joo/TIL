## `concat`
- 두 개의 문자열을 하나의 문자열로 만들어주는 역할

```
const str1 = "con";
const str2 = "cat";

const newStr = str1.concat(str2);
// 결과 : "concat"
```


 ## `filter`
 - 콜백함수에 지정된 조건에 맞는 요소를 새롭게 반환

```
const numbers = [1,2,3,4,5];
const biggerThanThree = numbers.filter(number => number > 3);
// 결과 : [4, 5]
```