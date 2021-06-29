



# 생성자 초기화 리스트(initializer list)

```c++
(class name) : var1(arg1), var2(arg2) {}
```

생성자 호출과 동시에 멤버 변수들을 초기화 해준다.

`var`  : 클래스 맴버 변수

`arg` :  멤버변수 초기화 값



#### 사용하는 이유 ?

생성자 초기화 리스트를 사용하지 않는 경우에는 __생성을 먼저하고 대입 한다.__

```c++
int a;
a = 10;
```

하지만 생성자 초기화 리스트를 사용하는 경우에는 __생성과 동시에 대입을 한다.__

```c++
int a = 10;
```



따라서 만약 타입이 클래스 일 경우에는 __전자의 경우 디폴트 생성자가 호출된 뒤 대입이 수행, 후자의 경우는 복사 생성자가 호출 된다.__

또한, `생성과 동시에 대입을 해야 하는 규칙`들이 있다. 대표적으로 래퍼런스 참조자 or 상수 이다. 따라서 이러한 키워드를 생성자에 표현 할떄에는 생성자 초기화 리스트를 사용해야 한다.



# static 

static 변수 또는 함수를 클래스 내부에 설정하면, 특정 객체에 종속되지 않고 클래스에 종속하게 된다. 한마디로 같은 클래스 내에서 static은 공유가 가능하다.

```c++
#include <iostream>

class TestStatic{
public:
    static int a;
    TestStatic(){a++;}
    ~TestStatic(){a--;}
    static void ShowA()
    {
        std::cout << a << std::endl;
    }

};
int TestStatic::a = 0;


int main() {
    TestStatic ts1;
    TestStatic ts2;
    TestStatic::ShowA();

    return 0;
}

/**
*[OutPut]
* 2
*/
```



위의 코드와 같이 a라는 static 변수는 클래스내에 종속 되므로 2가 출력된다. 또한 static 함수는 __{객체명}.{호출함수}__ 가 아닌 __{클래스}::{Static 함수}__ 로 호출 가능하다.



# this



### 레퍼런스를 리턴하는 함수 

```c++
// 레퍼런스를 리턴하는 함수
#include <iostream>

class A {
  int x;

 public:
  A(int c) : x(c) {}

  int& access_x() { return x; }
  int get_x() { return x; }
  void show_x() { std::cout << x << std::endl; }
};

int main() {
  A a(5);
  a.show_x();
  
  // 1.
  int& c = a.access_x();
  c = 4;
  a.show_x();

  // 2.
  int d = a.access_x();
  d = 3;
  a.show_x();

  // 3. 아래는 오류
  // int& e = a.get_x();
  // e = 2;
  // a.show_x();
  
  // 4.
  int f = a.get_x();
  f = 1;
  a.show_x();
}

/**
* [OutPut]
* 5
* 4
* 4
* 4
**/
```

위에 있는 코드를 차례대로 해석 하면,



#### 1.

```c++
 int& c = a.access_x();
 c = 4;
 a.show_x();
```

위 코드에 ``c`` 는 ``A 멤버변수(x)``의 레퍼런스(&)로 리턴을 받았기 때문에 ``x`` 에 별명이므로 값이 ``5`` 에서 ``4`` 로 변환한 걸 알 수있습니다. 또한 레퍼런스를 리턴하는 함수는 그 함수 부분을 원래의 변수로 치환했다고 생각해도 상관이 없다. 다시 말해서

```c++
int &c = x
```

와 동일하다. 또한,

```c++
a.access_x() = 3;
```

위 문장도 잘 작동된다. '레퍼런스를 리턴하는 함수는 그 함수 부분을 리턴하는 원래 변수로 치환해도 된다.' 라는 점에서 

```c++
a.x = 3;
```

와 동일한 말이다.





#### 2.

```c++
 int d = a.access_x();
 d = 3;
 a.show_x();
```

``d``에 타입이 레퍼런스가 아니므로, ``d``는 ``x``의 값만 복사 된다. 따라서 ``d``는 별명이 아닌 독립적인 변수이다.



#### 3.

```C++
// 아래는 오류 (error C2440: 'initializing' : cannot convert from 'int' to 'int &')
int& e = a.get_x();
e = 2;
a.show_x();
```

오류가 발생한다. 이유는 레퍼런스 타입이 아닌 경우에는 값이 __복사__ 되기 때문에 임시 객체가 생성되는데, 임시 객체는 레퍼런스를 생성할 수 없다.(문장이 끝나면 임시 객체는 소멸되기 떄문에 존재하지 않게 된다) 이러한 과정은 아래의 그림과 같다.

![image-20210628121718477](C:\Users\momantic03\AppData\Roaming\Typora\typora-user-images\image-20210628121718477.png)

#### 4.

```c++
int f = a.get_x();
f = 1;
a.show_x();
```

위의 코드는 임시로 생성된 `int` 변수 (위 그림에서는 `x'`) 값이 복사 되기 떄문에 `a` 의 `x` 의 아무런 영향이 없다. 또한,

```c++
a.get_x() = 3;
```

에러가 난다. 왜냐하면 리턴하면서 생성되는 임시 객체(x`)으로 치환되며 임시객체 대입을 하게 되는 모순적인 상황이 발생하기 떄문이다.



아래의 코드를 살펴보자.

```c++
#include <iostream>

class TestThis{
private:
    int x;
public:
    TestThis(int x) : x(x){}
    ~TestThis(){}
    TestThis(const TestThis &tt)
    {
        std::cout << "copy constructor : " << this << std::endl;
    }
    TestThis ThisFunction(const int x)
    {
        this->x -= x;
        std::cout << "tihs : " << this << std::endl;
        return *this;
    }
    TestThis& RefThisFunction(const int x)
    {
        this->x -= x;
        std::cout << "tihs : " << this << std::endl;
        return *this;
    }
    void PrintX()
    {
        std::cout << "x : " << x << std::endl;
    }

};


int main() {
    std::cout << "exam1)" << std::endl;
    TestThis t1(10);
    t1.ThisFunction(5).ThisFunction(3);
    t1.PrintX();

    std::cout << "======================================================= " << std::endl;
	
    std::cout << "exam2)" << std::endl;
    TestThis t2(10);
    t2.RefThisFunction(5).RefThisFunction(3);
    t2.PrintX();
    return 0;
}


```

```c++
[OutPut]

exam1)  
tihs : 0x62feb4
copy constructor : 0x62febc
tihs : 0x62febc
copy constructor : 0x62feb8
x : 5
=======================================================
    
exam2)
tihs : 0x62feb0
tihs : 0x62feb0
x : 2
```

#### exam1)

`t1(0x62feb4)` 이 호출한 함수 리턴값은 레퍼런스가 아니므로,  리턴타입 `TestThis` 가 `*this` 을 복사하면서 복사생성자가 호출된다. 따라서 임시 객체(__0x62febc__)의 `x` 값을 차감해준다. 결과적으로  `t1(0x62feb4)` 의 `x` 값을 변환 되지 않는다.



#### exam2)

`t2(0x62feb0)`가 호출한 함수 리턴값은 레퍼런스 이므로,  자기 자신(0x62feb0)의  함수 `.RefThisFunction(3)` 를 한번 더 호출하면서 `x`값을 차감해주면서 최종적으로 `2` 가 출력된다.



# const 함수

```c++
T t() const; // const function
```

위의 코드는 상수함수 형태를 선언하는 문법이다. 아래와 같이 읽기 전용으로 만들수 있다.

```c++
int Marine::attack() const { return default_damage; }
```

'상수 멤버 함수'로 선언하면 '읽기' 만이 수행되며, 상수 함수 내에서 호출 할 수 있는 함수로는 다른 상수 함수 밖에 없다.











__ref : https://modoocode.com/135__
