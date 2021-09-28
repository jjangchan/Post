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

