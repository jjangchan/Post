# friend 키워드

`friend` 키워드는 클래스 내부에서 **다른 클래스나 함수들을 friend** 로 정의하면 `private` 로 정의된 변수나 함수들에 접근할 수 있다.

```c++
#include <iostream>
#include <string>
#include "Example/Ex5MyString.h"

class A{
private:
    int a_num;
    void AFunction(){}
    
    // (B -> A) friend
    friend class B;
    
    //(func -> A) friend
    friend void func();
};

class B{
public:
    B(){
        A a;
        
        //친구이여서 접근 가능
        a.AFunction();
        a.a_num = 3;
    }
    
};

void func(){
    A a;
    
    // 친구이여서 접근 가능
    a.a_num = 5;
    a.AFunction();
}


int main(){
    return 0;
}

```

하지만  `A` 가 `B` 에 `private` 에는 접근할 수 없다.



# 이항 연산자

`operator` 를 멤버함수로 선언하고 이항 연산을 하면 문제점이 발생한다.

```c++
a = a + "1"; // 1번
```

은 잘 컴파일이 되서 실행 되는데,

```c++
a = "1" + a; // 2번
```

는 컴파일 되지 않는다. 왜냐하면 1번은 `a.operator+("1");` 으로 변환되지만 2번은 그렇지 못하기 때문이다. 이를 처리하기 위해서 외부함수로 선언해서 사용하면 된다.

```c++
Complex operator+(const Complex& a, const Complex& b){
	//..
}
```

인자로 `a, b` 를 받게 된다. 그러면 컴파일러는 정확히 일치 하지 않는 경우, 가장 가까운 *가능한* 오버로딩 되는 함수를 찾게 되는데, 마침 우리에게 `Complex(const char *)` 타입의 생성자가 있으므로,

```c++
operator+(Complex("1"), a);
```

가 되어서 실행된다. 그런데 문제는 외부함수이므로 `private` 멤버 변수를 접근해야한다. 따라서 이를 해결하기 위해서는 이 함수는 `Complex` 의 `friend` 로 지정하면 된다.

```c++
a = a+a;
```

을 컴파일하면 문제가 발생한다. 컴파일러는 해석할 때

```c++
a.operator+(a);
operator+(a, a);
```

두 가지 형태 중에서 하나를 골라야 하는데 모두 가능하기 때문에 모호해서 경고를낸다. 이를 해결 하기 위해서는 두 함수 중 하나를 없애야한다. 

통상적으로 자기 자신을 리턴하지 않는 이항 연산자들, 예를 들어 위와 같은 `+`, `-`, `*`, `/` 들은 모두 **외부 함수로 선언하는 것이 원칙** 입니다. 반대로 자기 자신을 리턴하는 이항 연산자들, 예를 들어 `+=`, `-=` 같은 애들은 모두 **멤버 함수로 선언하는 것이 원칙** 입니다. 

```c++
//
// Created by jjangchan on 2021/09/24.
//

#ifndef PSI_EX6COMPLEX_H
#define PSI_EX6COMPLEX_H

class Complex{
private:
    double real, img;
public:
    Complex(double real, double img):real(real), img(img){std::cout << "constructor : " << this << std::endl;}
    Complex(const Complex& c){real = c.real; img = c.img; std::cout << "copy constructor  : " << this << std::endl; std::cout << "c : " << &c << std::endl; }
    Complex(const char* str) {
        int begin = 0, end = strlen(str);
        img = 0.0;
        real = 0.0;

        //search i
        int pos_i = -1;
        for(int i = 0; i < end; i++) if(str[i] == 'i'){
                pos_i = i;
                break;
            }

        //only real
        if(pos_i == -1){
            real = GetNumber(str, begin, end-1);
            return;
        }

        // if "i" exists,
        real = GetNumber(str, begin, pos_i-1);
        img = GetNumber(str, pos_i+1, end-1);

        if(pos_i >= 1 && str[pos_i-1] == '-') img *= -1.0;
    }
    ~Complex(){}
    
    // -- 외부함수가 private를 접근할 수 있게 friend 키워드 사용 
    friend Complex operator+(const Complex& a, const Complex& b);
    friend Complex operator-(const Complex& a, const Complex& b);
    friend Complex operator*(const Complex& a, const Complex& b);
    friend Complex operator/(const Complex& a, const Complex& b);
    // --
  
  
    Complex& operator=(const Complex& c){
        real = c.real;
        img = c.img;
        return *this;
    }

    Complex& operator+=(const Complex& c){
        (*this) = (*this) + c;
        return *this;
    }

    Complex& operator-=(const Complex& c){
        (*this) = (*this) - c;
        return *this;
    }

    Complex& operator/=(const Complex& c){
        (*this) = (*this) / c;
        return *this;
    }

    Complex& operator*=(const Complex& c){
        (*this) = (*this) * c;
        return *this;
    }

    void println() const{
        std::cout << "( " << real << " , " << img << " )" << std::endl;
    }

private:
    double GetNumber(const char* str, int from, int to) const{
        bool minus = false;
        if(from > to) return 0;
        if(str[from] == '-') minus = true;
        if(str[from] == '-' || str[from] == '+') from++;

        double num = 0.0;
        double decimal = 1.0;

        bool integer_part = true;
        for(int i = from; i <= to; i++){
            if(isdigit(str[i]) && integer_part){
                num *= 10.0;
                num += (str[i] - '0');
            }else if(str[i] == '.') integer_part = false;
            else if(isdigit(str[i]) && !integer_part){
                decimal /= 10.0;
                num += ((str[i] - '0')*decimal);
            }else break;
        }
        if(minus) num *= -1.0;
        return num;
    }
};

// 자기자신을 리턴하지 않는 operator는 외부함수로 선언 !!
Complex operator+(const Complex& a , const Complex& b) {
    Complex temp(a.real+b.real, a.img+b.img);
    return temp;
}
Complex operator-(const Complex& a, const Complex& b) {
    Complex temp(a.real-b.real, a.img-b.img);
    return temp;
}
Complex operator*(const Complex& a, const Complex& b) {
    Complex temp(a.real * b.real - a.img * b.img, a.real * b.img + a.img * b.real);
    return temp;
}
Complex operator/(const Complex& a, const Complex& b) {
    Complex temp(
            (a.real * b.real + a.img * b.img) / (b.real * b.real + b.img * b.img),
            (a.img * b.real - a.real * b.img) / (b.real * b.real + b.img * b.img));
    return temp;
}

#endif //PSI_EX6COMPLEX_H

```



# 입출력 연산자 오버로딩 하기

iostream의 헤더파일의 내용을 보면 `ostream` 클래스에

```c++
ostream& operator<<(bool val);
ostream& operator<<(short val);
ostream& operator<<(unsigned short val);
ostream& operator<<(int val);
ostream& operator<<(unsigned int val);
ostream& operator<<(long val);
ostream& operator<<(unsigned long val);
ostream& operator<<(float val);
ostream& operator<<(double val);
ostream& operator<<(long double val);
ostream& operator<<(void* val);
```

와 같이 엄청난 수의 `operator<<` 가 정의되어 있다.

```c++
std::ostream& operator<<(std::ostream& os, const Complex& c) {
  os << "( " << c.real << " , " << c.img << " ) ";
  return os;
}
```

위와 같이 출력 클래스의  `ostream` 와 `Complex` 객체를 두개 받으면 출력이 가능해진다. 

```c++
friend ostream& operator<<(ostream& os, const Complex& c);
```

 `friend` 키워드를 사용해서 `real` 과 `img` 를 접근 가능하게 하면 된다.



# 첨자 연산자(operator[])
`oerator[]` 함수는 자명하게도 인자에 `int` 형을 인덱스로 받으면된다.
```c++
char& operator[](const int index){return string_content[index];}
```
위의 함수를 호출하면  `return` 받고 수정할 내용을 대입시키면 된다.
```c++
int main() {
  MyString str("abcdef");
  str[3] = 'c';

  str.println();
}
```
출력은 아래와 같다.
```
abccef
```



# 타입 변환 연산자

타입 변환 연산자는 클래스의 객체를 마치 '`int` 형 변수'라고 컴파일러에게 알려준다. 
타입 변환 연산자의 정의는 아래와 같다.
```c++
operator T()
```
주의점은 생성자 처럼 `return` type을 써주면 안된다.

`int`형 `Wrapper` 클래스를 만들면 아래와 같다.

```c++
class Int{
private:
    int num;
public:
    Int(int num): num(num){}
    Int(const Int& i): num(i.num){}
    operator int(){return num;}
};


int main() {
    Int x = 3;
    int a = x + 4;

    x = a * 2 + x + 4;
    std::cout << x << std::endl;
    return 1;
}
```
```
24
```



# 전위/후위 증감 연산자

전위 증감 연산자는 **값이 바뀐 자기 자신**을 리턴하고, 후의 증감의 경우 **값이 바뀌기 이전의 객체**를 리턴하면 된다. 따라서 후의 증감 연산은 객체를 복사하기 때문에 속도가 전위 증감 연산자 보다 더 느리다. 
```c++
#include <iostream>

class Test{
private:
    int num;
public:
    Test(int num): num(num){}
    Test(const Test& i): num(i.num){}
    Test& operator++(){
        num++;
        std::cout << "전위 증감 연산자 호출" << std::endl;
        return (*this);
    }

    Test operator++(int){
        Test temp(num);
        num++;
        std::cout << "후의 증감 연산자 호출" << std::endl;
        return temp;
    }

    int getNum() const{return num;}
};

void println(const Test& t){
    std::cout << "num : " << t.getNum() << std::endl;
}

int main() {
    Test t(3);
    println(++t);
    println(t++);
    println(t);
    return 1;
}
```
```
전위 증감 연산자 호출
num : 4
후의 증감 연산자 호출
num : 4
num : 5
```



# 정리

연산자 오버로딩에 대해 다루면서 몇 가지 중요한 포인트 들만 따로 정리해보자면;

- 두 개의 동등한 객체 사이에서의 이항 연산자는 멤버 함수가 아닌 외부 함수로 오버로딩 하는 것이 좋습니다. (예를 들어 `Complex` 의 `operator+(const Complex&, const Complex&) const` 와 같이 말입니다.)
- 두 개의 객체 사이의 이항 연산자 이지만 한 객체만 값이 바뀐다던지 등의 동등하지 않는 이항 연산자는 멤버 함수로 오버로딩 하는 것이 좋습니다. (예를 들어서 `operator+=` 는 이항 연산자 이지만 `operator+=(const Complex&)` 가 낫다)
- 단항 연산자는 멤버 함수로 오버로딩 하는 것이 좋습니다 (예를 들어 `operator++` 의 경우 멤버 함수로 오버로딩 합니다)
- 일부 연산자들은 반드시 멤버 함수로만 오버로딩 해야 합니다 (강좌 앞 부분 참고)




> 출처
>
> https://modoocode.com/135

