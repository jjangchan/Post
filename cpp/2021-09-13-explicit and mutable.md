# explicit



## 암시적 변환(implicit conversion)

```c++
#include <string>

class ExplicitTest{
private:
    std::string str;
    char c;
public:
    //constructor
    ExplicitTest(const char* str){
        this->str = str;
    }

    ExplicitTest(const char c){
        this->c = c;
    }

    //copy constructor
    ExplicitTest(const ExplicitTest& copy){
        str = copy.str;
        c = copy.c;
    }

    //destructor
    ~ExplicitTest(){}
};

void TestFunction(ExplicitTest test){}


int main() {
    // 암시적 변환
    TestFunction(ExplicitTest("abc"));
    TestFunction("abc");
    return 0;
}
```



```c++
TestFunction(ExplicitTest("abc"));
```

이 코드는 `ExplicitTest` 객체를 생성해서 인자로 전달해서 컴파일이 됩니다.



```c++
TestFunction("abc");
```

c++ 컴파일러는 `ExplicitTest`  클래스에 `const char* str` 인자로 받는 생성자가 있으므로 변환되서 컴파일이 된다. 위와 같은 변환을 **암시적 변환(implicit conversion)** 이라고 부른다.



## 암시적 변환의 문제점

```c++
TestFunction(3);
```

 `ExplicitTest` 클래스에 `const char c` 인자로 받는 생성자가 있으므로 함수의 오버로딩 규칙 떄문에 컴파일이 된다. 사용자가 의도하지 않은 암시적 변환가 되였다. 

c++에서는 원하지 않은 암시적 변환을 할 수 없도록 컴파일러에게 명시할 수 있다. 

```c++
#include <string>

class ExplicitTest{
private:
    std::string str;
    char c;
public:
    //constructor
    ExplicitTest(const char* str){
        this->str = str;
    }

    explicit ExplicitTest(const char c){
        this->c = c;
    }

    //copy constructor
    ExplicitTest(const ExplicitTest& copy){
        str = copy.str;
        c = copy.c;
    }

    //destructor
    ~ExplicitTest(){}
};

void TestFunction(ExplicitTest test){}


int main() {
   	TestFunction('c'); // error
    return 0;
}
```

바로 `explicit` 키워드를 사용해서 막을수 있다. 따라서 컴파일 오류가 발생한다. 

`explicit` 은 `implicit` 의 반대말로, 명시적 이라는 뜻을 가지고 있다. 

`explicit` 은 또한 해당 생성자가 복사 생성자의 형태로도 호출되는 것을 막게 된다.

```c++
ExplicitTest test('c'); // 허용
ExplicitTest test = 'c' // 컴파일 오류
```



# mutable

`const` 멤버 함수는 멤버 변수들의 값을 바꾸는것을 불가능 하다. 하지만, 만약에 멤버 변수를 `mutable` 로 선언하면 **const 함수에서도 이들 값을 바꿀 수 있다.**

```c++
#include <iostream>

class MutableTest{
private:
    mutable int a;
public:
    MutableTest(int a) : a(a){}
    void TestFunction(int x) const{
        a = x; // 가능 
    }

    void Println() const {std::cout << "a : " << a << std::endl;}
};



int main() {
    MutableTest t(3);
    t.Println();
    t.TestFunction(5);
    t.Println();
    return 0;
}
```

멤버 변수 a는 `mutable` 키워드를 사용해서 `const` 멤버 함수에서도 수정이 가능하다.



## mutable를 사용하는 이유

```c++
class Server {
  // .... (생략) ....

  Cache cache; // 캐쉬!

  // 이 함수는 데이터베이스에서 user_id 에 해당하는 유저 정보를 읽어서 반환한다.
  User GetUserInfo(const int user_id) const {
    // 1. 캐쉬에서 user_id 를 검색
    Data user_data = cache.find(user_id);

    // 2. 하지만 캐쉬에 데이터가 없다면 데이터베이스에 요청
    if (!user_data) {
      user_data = Database.find(user_id);

      // 그 후 캐쉬에 user_data 등록
      cache.update(user_id, user_data); // <-- 불가능
    }

    // 3. 리턴된 정보로 User 객체 생성
    return User(user_data);
  }
};
```

`update` 함수는 `const` 함수가 아니므로 호출이 불가능하다.

```c++
cache.update(user_id, user_data); // <-- 불가능
```

사용자 입장에서 `GetUserInfo` 함수는 읽기전용 함수이므로 `const`로 정의 하는게 맞기 때문에, 이를 해결하기 위해서 `cache` 에 `mutable`로 선언하면 된다.

```c++
mutable Cache cache; // 캐쉬!
```





> 출처
>
> https://modoocode.com/135

