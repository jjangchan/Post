# 복사 생성자(Copy Constructor)



```c++
T(const T& t)
```

__위는 복사 생성자의 표준적인 정의이다. *const* 이기 때문에 우리는 복사 생성자 내부에서 t의 값을 변경할 수 없고, 오직 새롭게 초기화 되는 인스턴스 변수들에게만 '복사' 만 할 수 있게 된다.__



# 디폴트 복사 생성자(Defaul copy constructor)

c++ 컴파일러는 이미 __디폴트 복사 생성자(Default copy constructor)__ 를 지원해주고 있다. 선언 하지 않아도 알아서 인스턴스 변수들을 복사해준다.



### 한계

```c++
#include <string.h>

class PC{
private:
    char *name;
public:

    PC(const char *name){
        this->name = new char[strlen(name)+1];
        strcpy(this->name, name);
    };
    ~PC(){
        if(name) {
            delete[] name;
            std::cout << "delete.." << std::endl;
        }
    };
};

int main() {
    PC p1("pc1");
    PC p2 = p1;
    return 0;
}
```

디폴트 복사 생성자는 대입만 해주는 __얕은 복사(shallow copy)__ 를 해주므로 name(char) 에 메모리를 공유하게 된다. 따라서 소멸자가 호출하면 delete를 두번 해주면서 Block이 걸리면서 런타임 에러(이상하게 CLion에서는 에러가 안 난다..)를 발생 시킨다.





### 해결방법

복사생성자를 직접 선언 하고 메모리를 공유하지말고 직접 동적으로 할당 받으면 된다. 메모리를 새로 할당해서 내용을 복사하는것을 __깊은 복사(deep copy)__ 라고 한다.

```c++
#include <string.h>

class PC{
private:
    char *name;
public:
	// Constructor
    PC(const char *name){
        this->name = new char[strlen(name)+1];
        strcpy(this->name, name);
    };
	
    // Copy Constructor
    PC(const PC &pc){
        //deep copy....
        this->name = new char[strlen(pc.name)+1];
        strcpy(this->name, pc.name);
    }
	// Destructor
    ~PC(){
        if(name) {
            delete[] name;
            std::cout << "delete.." << std::endl;
        }
    };
};


int main() {
    PC p1("pc1");
    PC p2 = p1;

    return 0;
}
```



__ref : https://modoocode.com/135__
