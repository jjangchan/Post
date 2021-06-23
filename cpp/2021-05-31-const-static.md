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



__ref : https://modoocode.com/135__



# Static 

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

