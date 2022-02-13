# Map 컬렉션 for-each 문

```cpp
map<string, int> m;

for (auto it : m) {
    cout << "Key : " << it.first << " Value : " << it.second << "\n";
}
```

자바는 C++ 처럼 `auto` 키워드를 지원하지 않아서 위와 같은 코드를 사용하지 못해서 Java 공식 문서를 보고 `for-each` 문을 사용하는 방법을 정리하려고 한다.

## 데이터 생성

```java
Map<String, Integer> map = new HashMap<String, Integer>();
map.put("a", 1);
map.put("b", 2);
map.put("c", 3);
```

## `Interator` 클래스 사용

```java
Interator<String> keys = map.keySet().iterator();
while (keys.hasNext()) {
    String key = keys.next();
    String value = map.get(key);
    System.out.println(key + " : " + value);
}
```

## `Map` method 사용

### `Map.keySet()`

```java
for (String key : map.keySet()) {
    String value = map.get(key);
    System.out.println(key + " : " + value);
}
```

### `Map.Entry<>`

```java
for (Map.Entry<String, Integer> m : map.entrySet()) {
    String key = m.getKey();
    String value = map.get(key);
    System.out.println(key + " : " + value);
}
```

### `map.forEach()`

```java
map.forEach((key, value) -> {
    System.out.println(key + " : " + value);
});
```

# String for-each 문
자바에서 문자열 for-each 문을 사용하려면 `.toCharArray()` 메서드를 사용해야한다.
```java
String str = "abcd"

for (char c : str.toCharArray()) {
    ...
}
```