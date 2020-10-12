# c++에서 split 사용하기

`sstream` 헤더파일 필요  
`isstringstream`과 `getline` 함수를 사용하여 분할

    #include <string>
    #include <iostream>
    #include <sstream>
        
    using namespace std;

    int main() {
        // c++ string split
        string as = "this,is,string";
        istringstream ss(as);
        string stringBuffer;
        while (getline(ss, stringBuffer, ',')) {
            cout << stringBuffer << " ";
        }
        return 0;
     }
