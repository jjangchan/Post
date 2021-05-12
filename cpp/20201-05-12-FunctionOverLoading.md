# 함수의 오버로딩(Function overloading)



#### 함수의 오버로딩 이란, '이름이 동일한 함수의 인자를 다르게 하여서 과부하를 주는것이다.'

```c++
/* 함수의 오버로딩 */

#include <iostream>

class Point{
private:
    
public:
    /** constructor overloading **/
    Point(int a, int b){}
    Point(double a, double b){}
    Point(char a, char b){} 
private:
};

```



#### C++ 컴파일러 함수를 오버로딩하는 과정



__1 단계__

자신과 타입이 정확히 일치하는 함수를 찾는다.



__2 단계__

정확히 일치하는 타입이 없는 경우, 아래와 같은 형변환을 통해서 일치하는 함수를 찾는다.

- `Char, unsigned char, short` 는 `int` 로 변환된다.
- `Unsigned short` 는 `int` 의 크기에 따라 `int` 혹은 `unsigned int` 로 변환된다.
- `Float` 은 `double` 로 변환된다.
- `Enum` 은 `int` 로 변환된다.



__3 단계__

위와 같이 변환해도 일치하는 것이 없다면 아래의 좀더 포괄적인 형변환을 통해 일치하는 함수를 찾는다.

- 임의의 숫자(numeric) 타입은 다른 숫자 타입으로 변환된다. (예를 들어 `float -> int)`
- `Enum` 도 임의의 숫자 타입으로 변환된다 (예를 들어 `Enum -> double)`
- `0` 은 포인터 타입이나 숫자 타입으로 변환된 0 은 포인터 타입이나 숫자 타입으로 변환된다
- 포인터는 `void` 포인터로 변환된다



__4 단계__

유저 정의된 타입변환으로 일치하는 것을 찾는다

만약에 컴파일러가 위 과정을 통하더라도 일치하는 함수를 찾을 수 없거나 같은 단계에서 __두 개 이상이 일치__ 하는 경우에 

__모호하다(ambiguous)__ 라고 판단해서 오류를 발생하게 된다.

```c++
using namespace std;

#include <iostream>

void Print(int x) {cout << "int : " << x << endl;}
void Print(char x) {cout << "char : " << x << endl;}

int main() {
    int a = 1;
    char b = 'a';
    double c= 3;

    Print(a);
    Print(b);
    Print(c);

    return 0;
}

// double 은 3단계에 의해 char 도, int 도 변환 됨,
// 따라서 error: call of overloaded 'Print(double&)' is ambiguou
```

