# 상속(Inheritance)

c++ 에서 상속을 통해 다른 클래스의 정보를 물려 받아서 사용할 수 있다.



## 1. 상속 선언

기반 클래스를 선언하고,

```c++
class Base{
private:
    std::string s;
public:
    Base() : s("base"){ std::cout << "base class" << std::endl;}
    void println() const {std::cout << s << std::endl;}

};

```

아래와 같이 파생클래스를 상속 받으면 된다.

```c++
class Derived : public Base{
private:
    std::string s;
public:
    Derived() : Base(), s("derived") {
        std::cout << "derive" << std::endl;
        println();
    }
};
```

여기서 `Derived` 가 `Base` 를 `public` 형식으로 상속 받는 뜻이다. 따라서 `Derived` 는 `Base` 클래스의 `println` 함수를 호출할수 있게 된다.



생성자 초기화 리스트에서 기반의 생성자를 호출해서 기반의 생성을 먼저 처리하고, `Dervied` 의 생성자가 실행 되어야 한다.

```c++
erived() : Base(), s("derived")
```

만약 기반 클래스의 생성자를 명시적으로 호출하지 않으면 기반 클래스의 **디폴트 생성자가 호출된다.**



## 2. 오버라이딩(Overriding)

만약 기반 클래스에도 `println` 함수를 선언하면 어떻게 될까?

```c++
class Base{
private:
    std::string s1;
public:
    Base() : s1("base"){ std::cout << "base class" << std::endl;}
    void println() const {std::cout << s1 << std::endl;}

};

class Derived : public Base{
private:
    std::string s;
public:
    Derived() : Base(), s("derived") {
        std::cout << "derived class" << std::endl;
        println();
    }

    void println() const {std::cout << s << std::endl;}
};

int main() {
    Base p;
    Derived d;
    return 1;
}
```

```
base class
base class
derived class
derived
```

위 경우에는 `Derived` 에  `println` 함수가 선언되어 있기 때문에 굳이 멀리 있는 `Base` 의 함수 까지 뒤지지 않고, 바로 앞에 있는 `Derived` 의  `println` 함수를 호출하게된다. 

`Derived` 의 `println` 함수가  `base` 의  `println` 함수를 **오버라이딩(overriding)** 한것이다.



## 3. Protected 

```c++
class Base{
private:
    std::string s1;
public:
    Base() : s1("base"){ std::cout << "base class" << std::endl;}
    void println() const {std::cout << s1 << std::endl;}

};

class Derived : public Base{
private:
    std::string s;
public:
    Derived() : Base(), s("derived") {
        std::cout << "derived" << std::endl;
        println();
        s1 = "aaa"; // error : string Base::s1' is private within this context
    }

    void println() const {std::cout << s << std::endl;}
};
```

기반 클래스의 `s1` 은 수정할 수 없다. 왜냐하면 `private` 키워드 때문에 자기 자신 말고는 접근할 수 없다. 따라서 `protected` 라는 키워드를 사용한다. 이 키워드는 **속받는 클래스에서는 접근 가능하고 그 외의 기타 정보는 접근 불가능** 이라고 보시면 된다.



## 4. 상속 접근 지시자 키워드

처음 상속할 때 접근 지시자 키워드를 사용한다.

```c++
class Derived : public Base
```

여기서 키워드가  `public` , `protected`, `private` 에 따라 상속 받는 클래스에서 기반 클래스의 멤버들이 실제로 어떻게 작동하는지 영향을 준다.

- 만일 위처럼 `public` 형태로 상속 하였다면 기반 클래스의 접근 지시자들에 영향 없이 그대로 작동합니다. 즉 파생 클래스 입장에서 `public` 은 그대로 `public` 이고, `protected` 는 그대로 `protected` 이고, `private` 은 그대로 `private` 입니다.
- 만일 `protected` 로 상속하였다면 파생 클래스 입장에서 `public` 은 `protected` 로 바뀌고 나머지는 그대로 유지됩니다.
- 만일 `private` 으로 상속하였다면 파생 클래스 입장에서 모든 접근 지시자들이 `private` 가 됩니다.

아래 예제를 통해 알아보자,

```c++
class Base{
public:
    std::string s1;
public:
    Base() : s1("base"){ std::cout << "base class" << std::endl;}
    void println() const {std::cout << s1 << std::endl;}

};

class Derived : private Base{
private:
    std::string s;
public:
    Derived() : Base(), s("derived") {
        std::cout << "derived" << std::endl;
    }

    void println() const {std::cout << s << std::endl;}
};

int main() {
    Base p;
    // 기반 클래스를 통해서는 public 이므로 접근 가능
    p.s1;
    Derived d;
    // 파생 클래스 에서는 (private 로 상속 받았기 때문에) private가 되어서 접근 불가능
    d.s1;
    
    return 1;
}
```



## 5. is 'a' & has 'a'

클래스의 `is - a ` 관계에는 2가지 상속의 특징이 있다.

1. 클래스가 파생되면 파생될 수록 좀더 **특수화 (구체화;specialize**된다.
2. 기반 클래스로 거슬러 올라가면 올라갈 수록 좀 더 **일반화 (generalize)**  된다.

 `has -a` 관계 또한 갖는다. 예를들면 아래와 같이 자동차 클래스로 만들면 자동차 클래스를 구성하기 위해서는 엔진 클래스, 브레이크 클래스, 오디오 클래스 등 수 많은 클래스들이 필요하다.

```c++
class Car {
 private:
  Engine e;
  Brake b;  
  ....
};
```



## 6. 업 캐스팅 & 다운 캐스팅

```c++
class Base{
public:
    std::string s1;
public:
    Base() : s1("base"){ std::cout << "base class" << std::endl;}
    void println() const {std::cout << s1 << std::endl;}

};

class Derived : public Base{
private:
    std::string s;
public:
    Derived() : Base(), s("derived") {
        std::cout << "derived class" << std::endl;
    }
    void println() const {std::cout << s << std::endl;}
};

int main() {
    Base b;
    Derived d;

    Base* p = &d;
    p->println();
    return 1;
}

```

```
base class
base class
derived class
base
```

위 와 같이 `Base*` 에 `d` 의 주소값을 대입하면 `Base` 의 `println` 함수가 호출된다. 왜냐하면

![Inheritance1](../img/Inheritance1.JPG)

위의 그림과 같이 `p` 는 엄연한 `Base` 객체를 가리키는 포인터 이다.

이러한 형태의 캐스팅을(즉 파생 클래스에서 기반 클래스로 캐스팅 하는 것)을 **업 캐스팅** 이라고 불른다.



만약 **다운 캐스팅**도 할 수 있을까?

```c++
class Base{
public:
    std::string s1;
public:
    Base() : s1("base"){ std::cout << "base class" << std::endl;}
    void println() const {std::cout << s1 << std::endl;}

};

class Derived : public Base{
private:
    std::string s;
public:
    Derived() : Base(), s("derived") {
        std::cout << "derived class" << std::endl;
    }
    void println() const {std::cout << s << std::endl;}
};

int main() {
    Base b;
    Derived d;

    Derived* p_d = &b;
    p_d->println(); //error : 'initializing' : cannot convert from 'Base *' to 'Derived *'

    return 1;
}
```

컴파일 오류가 난다. 



![Inheritance2](../img/Inheritance2.JPG)

`p_d` 의 객체가 가리키는 객체는 `Base` 이므로 `Derived` 에 대한 정보가 없다. 따라서 컴파일러 상에서 함부로 다운 캐스팅 하는 것을 금지하고 있다.

```c++
class Base{
public:
    std::string s1;
public:
    Base() : s1("base"){ std::cout << "base class" << std::endl;}
    void println() const {std::cout << s1 << std::endl;}

};

class Derived : public Base{
private:
    std::string s;
public:
    Derived() : Base(), s("derived") {
        std::cout << "derived class" << std::endl;
    }
    void println() const {std::cout << s << std::endl;}
};

int main() {
    Base b;
    Derived d;

    Base* p_b = &d;
    Derived* p_d= &p_b;
    
    p_d->println();
    return 1;
}
```

근본적으로 `p_b` 가 가리키는 객체는 `Derived` 인데도 컴파일러 오류가 난다. 만약 강제적으로 타입 변환하면 어떻게 될까?

```c++
 Derived* p_d= static_cast<Derived*>(p_b);
```

비록 약간은 위험하지만 컴파일 오류를 발생시키지 않고 성공적으로 컴파일 할 수 있다.