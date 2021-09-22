# 연산자 오버로딩(operator overloading)



## 선언 방법

아래와 같은 규칙으로 연산자 오버로딩 함수를 선언할 수 있다.

```
(리턴 타입) operator(연산자) (연산자가 받는 인자)

bool operator==(Test& t){ return a == t.a;}
```

`t1 == t2` 라고 명령을 하게 된다면 위에 `oprator==` 로 내부적으로 변환하면서 호출하여 코드를 수행하면서 반환하게 된다.

```c++
#include <iostream>

class Test{
private:
    int a;
public:
    Test(int a) : a(a){}
    ~Test(){}
    bool operator==(Test& t){
        return a == t.a;
    }
};


int main(){
    Test t1(3);
    Test t2(2);

    if(t1 == t2) std::cout << "equals";
    else std::cout << "not equals";
    std::cout << std::endl;

    // OutPut : not equals

    Test t3(1);
    Test t4(1);

    if(t3 == t4) std::cout << "equals";
    else std::cout << "not equals";

    // OutPut : equals

    return 0;
}
```

