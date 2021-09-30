# 연산자 오버로딩(operator overloading)



## 선언 방법

아래와 같은 규칙으로 연산자 오버로딩 함수를 선언할 수 있다.

```
(리턴 타입) operator(연산자) (연산자가 받는 인자)

bool operator==(Test& t){ return a == t.a;}
```

`t1 == t2` 라고 명령을 하게 된다면 `t1.operator==(t2)` 로 내부적으로 변환되서 처리된다.

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



## 연산자 오버로딩 선언과 호출 순서

```c++
#include <iostream>

class Complex{
private:
    double real, img;
public:
    Complex(int real, int img):real(real), img(img){
      std::cout << "constructor : " << this << std::endl;
    }
    Complex(const Complex& c){
      real = c.real; 
      img = c.img; 
      std::cout << "copy constructor  : " << this << std::endl; 
      std::cout << "c : " << &c << std::endl; 
    }
    ~Complex(){}
    Complex operator+(const Complex c) const {
        Complex temp(real+c.real, img+c.img);
        return temp;
    }
    Complex operator-(const Complex c) const {
        Complex temp(real-c.real, img-c.img);
        return temp;
    }
    Complex operator*(const Complex c) const {
        std::cout << "previous temp " << std::endl;
        Complex temp(real*c.real-img*c.img, real*c.img+c.real*img);
        std::cout << "operator constructor : " << &temp << std::endl;
        return temp;
    }
    Complex operator/(const Complex c) const {
        Complex temp(
                (real*c.real+img*c.img)/(c.real*c.real+c.img*c.img),
                (c.real*img-real*c.img)/(c.real*c.real+c.img*c.img));
        return temp;
    }

    void println() const{
        std::cout << "( " << real << " , " << img << " )" << std::endl;
    }
};

int main(){
    Complex c1(1.0, 2.0);
    std::cout << " ->" << &c1 << std::endl;
    Complex c2(3.0, -2.0);
    std::cout << " ->" << &c2 << std::endl;
    Complex c3 = c1 * c2;
    std::cout << " ->" << &c3 << std::endl;
    
    /** out put
    constructor : 0x7ffeeabbfa58
 			->0x7ffeeabbfa58
		constructor : 0x7ffeeabbfa38
 			->0x7ffeeabbfa38
		copy constructor  : 0x7ffeeabbfa18
		c : 0x7ffeeabbfa38
		previous temp 
		constructor : 0x7ffeeabbfa28
		operator constructor : 0x7ffeeabbfa28
 			->0x7ffeeabbfa2
    **/
    
    return 0;
}
```

**호출 순서를 알아보자,**

1. `c1(0x7ffeeabbfa58)` 생성자 호출
2. `c2(0x7ffeeabbfa38)` 생성자 호출
3. `c3(0x7ffeeabbfa18)` 복사생성자 호출, 인자로 받은 값은 `c2`  이다.
4. `operator` 함수 호출
5. `temp(0x7ffeeabbfa28)` 생성자 호출, **! 임시객체의 복사생성자는 생략됨**
6. `c3` 에 `temp` 값 대입



## 대입 연산자 함수

자기 자신을 가리키는 레퍼런스로을 리턴해야한다. 왜냐하면

```c++
a = b = c;
```

위와 같은 코드로 `b = c;` 가 `b` 를 리턴해야지, `a = b;` 가 성공적으로 수행되기 때문이다. 따라서 대입 연산 이후에 불필요한 복사를 방지하기 위해선 자기자신 `&` 으로 리턴하면 된ß다. 

```c++
Complex& Complex::operator=(const Complex& c)
{
  real = c.real;
  img = c.img;
  return *this;
}
```

대입 연산자 함수는 디폴트 대입 연산자(default assignment operator)를 지원하고 있다. 디폴트 대입 연산자는 디폴트 복사 생성자와 마찬가지로 얕은 복사를 수행하기 때문에, 깊은 복사가 필요하면 선언해서 관리를 해줘야한다.

```c++
A a = b; // 1번
```

와

```c++
A a; // 2번
a = b;
```

의 차이점은

1번은 복사생성자가 호출되고, 2번은 생성자가 호출하고 대입연산자가 호출된다.



## 문자열 리터럴 연산자 오버로딩

```c++
#include <iostream>
#include <cstring>

class Complex {
 private:
  double real, img;

  double get_number(const char* str, int from, int to) const;

 public:
  Complex(double real, double img) : real(real), img(img) {}
  Complex(const Complex& c) { real = c.real, img = c.img; }
  Complex(const char* str);

  Complex operator+(const Complex& c) const;
  Complex operator-(const Complex& c) const;
  Complex operator*(const Complex& c) const;
  Complex operator/(const Complex& c) const;

  Complex& operator+=(const Complex& c);
  Complex& operator-=(const Complex& c);
  Complex& operator*=(const Complex& c);
  Complex& operator/=(const Complex& c);

  Complex& operator=(const Complex& c);

  void println() {
    std::cout << "( " << real << " , " << img << " ) " << std::endl;
  }
};
Complex::Complex(const char* str) {
  // 입력 받은 문자열을 분석하여 real 부분과 img 부분을 찾아야 한다.
  // 문자열의 꼴은 다음과 같습니다 "[부호](실수부)(부호)i(허수부)"
  // 이 때 맨 앞의 부호는 생략 가능합니다. (생략시 + 라 가정)

  int begin = 0, end = strlen(str);
  img = 0.0;
  real = 0.0;

  // 먼저 가장 기준이 되는 'i' 의 위치를 찾는다.
  int pos_i = -1;
  for (int i = 0; i != end; i++) {
    if (str[i] == 'i') {
      pos_i = i;
      break;
    }
  }

  // 만일 'i' 가 없다면 이 수는 실수 뿐이다.
  if (pos_i == -1) {
    real = get_number(str, begin, end - 1);
    return;
  }

  // 만일 'i' 가 있다면,  실수부와 허수부를 나누어서 처리하면 된다.
  real = get_number(str, begin, pos_i - 1);
  img = get_number(str, pos_i + 1, end - 1);

  if (pos_i >= 1 && str[pos_i - 1] == '-') img *= -1.0;
}
double Complex::get_number(const char* str, int from, int to) const {
  bool minus = false;
  if (from > to) return 0;

  if (str[from] == '-') minus = true;
  if (str[from] == '-' || str[from] == '+') from++;

  double num = 0.0;
  double decimal = 1.0;

  bool integer_part = true;
  for (int i = from; i <= to; i++) {
    if (isdigit(str[i]) && integer_part) {
      num *= 10.0;
      num += (str[i] - '0');
    } else if (str[i] == '.')
      integer_part = false;
    else if (isdigit(str[i]) && !integer_part) {
      decimal /= 10.0;
      num += ((str[i] - '0') * decimal);
    } else
      break;  // 그 이외의 이상한 문자들이 올 경우
  }

  if (minus) num *= -1.0;

  return num;
}
Complex Complex::operator+(const Complex& c) const {
  Complex temp(real + c.real, img + c.img);
  return temp;
}
Complex Complex::operator-(const Complex& c) const {
  Complex temp(real - c.real, img - c.img);
  return temp;
}
Complex Complex::operator*(const Complex& c) const {
  Complex temp(real * c.real - img * c.img, real * c.img + img * c.real);
  return temp;
}
Complex Complex::operator/(const Complex& c) const {
  Complex temp(
      (real * c.real + img * c.img) / (c.real * c.real + c.img * c.img),
      (img * c.real - real * c.img) / (c.real * c.real + c.img * c.img));
  return temp;
}

Complex& Complex::operator+=(const Complex& c) {
  (*this) = (*this) + c;
  return *this;
}
Complex& Complex::operator-=(const Complex& c) {
  (*this) = (*this) - c;
  return *this;
}
Complex& Complex::operator*=(const Complex& c) {
  (*this) = (*this) * c;
  return *this;
}
Complex& Complex::operator/=(const Complex& c) {
  (*this) = (*this) / c;
  return *this;
}
Complex& Complex::operator=(const Complex& c) {
  real = c.real;
  img = c.img;
  return *this;
}

int main() {
  Complex a(0, 0);
  a = a + "-1.1 + i3.923";
  a.println();
  a = a - "1.2 -i1.823";
  a.println();
  a = a * "2.3+i22";
  a.println();
  a = a / "-12+i55";
  a.println();
}
```

컴파일 한다면,

```c++
( -1.1 , 3.923 ) 
( -2.3 , 5.746 ) 
( -131.702 , -37.3842 ) 
( -0.150113 , 2.42733 ) 
```

결과가 나온다. 문자열 리터럴을 자동적으로 컴파일러가 알아서 생성자를 호출해준다. 아래의 문장을 사용하면,

```c++
a = a + "-1.1 + i3.923";
```

컴파일러는

```c++
a = a.operator+(Complex("-1.1 + i3.923"));
```

로 바꿔준다. 그리고 `operator+`  함수의 인자가 `const` 가 아니면 위와 같은 변환은 이루어지지 않는다. 왜냐하면 `-1.1+i3.923` 자체가 문자열 리터럴 이므로, 이를 바탕으로 생성된 객체 역시 상수 여야 하기 떄문이다.

