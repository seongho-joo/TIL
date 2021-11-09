# 대 소문자 판단하기
```cpp
string s = "AbCd";

for(auto c : s) {
  if(isupper(c)) cout << "uppercase\n";
  else cout << "lowercase\n";
}
/** 출력
  uppercase
  lowercase
  uppercase
  lowercase
*/
```

# 대문자 소문자 바꾸기
```cpp
string s = "AbCd";

for(auto &c : s) {
  if(isupper(c)) c = tolower(c);
  else c = toupper(c);
}

cout << s; // "aBcD"
```