## unique_ptr

`객체`를 포인터 `객체` 로 만들어서, 스택의 객체가 자원을 반납할 때 소멸자로 자신이 가리키는 모든 데이터를 `delete` 하게 된다. 자원 관리를 스택에 할당한 객체를 통해 하는 방식을을 `RAII(Resource Acquisition is initializtion)` 이라고 한다. `unique_ptr` 을 RAII 방식으로 자원을 관리 하므로, 특정 객체에 유일한 소유권을 부여하는 포인터 객체이다.

`unique_ptr` 은 복사생성자를 금지 하고 있다.



## 삭제된 함수

```c++
#include <iostream>


class A {
 public:
  A(int a){};
  A(const A& a) = delete;
};

int main() {
  A a(3);  // 가능
  A b(a);  // 불가능 (복사 생성자는 삭제됨)
}
```

복사 생성자에 `delete` 키워드를 사용하면, 복사 생성자를 명시적으로 삭제한다. 따라서 만약에 사용하더라도 컴파일에서 오류가 발생한다. `unique_ptr` 또한 유일한 객체를 소유 하려고 복사 생성자를 금지 하였다. 복사 생성자를 삭제된 이유는 소멸된 객체를 다시 소멸시켜서 발생하는 버그 `double free` 를 방지 하고, 말 그대로 유일하게 객체를 소유해야 하기 때문이다.



## unique_ptr 소유권 이전하기

하지만, `unique_ptr` 은 복사는 안되지만, 소유권은 이전할 수 있다.

```c++
#include <iostream>
#include <memory>

class A {
  int *data;

 public:
  A() {
    std::cout << "자원을 획득함!" << std::endl;
    data = new int[100];
  }

  void some() { std::cout << "일반 포인터와 동일하게 사용가능!" << std::endl; }

  ~A() {
    std::cout << "자원을 해제함!" << std::endl;
    delete[] data;
  }
};

void do_something() {
  std::unique_ptr<A> pa(new A());
  std::cout << "pa : ";
  pa->some();

  // pb 에 소유권을 이전.
  std::unique_ptr<A> pb = std::move(pa);
  std::cout << "pb : ";
  pb->some();
  
  std::cout << "pa(address) : " << pa.get() << std::endl;
  std::cout << "pb(address) : " << pb.get() << std::endl;
}

int main() { do_something(); }
```

```shell
[OutPut]

자원을 획득함!
pa : 일반 포인터와 동일하게 사용가능!
pb : 일반 포인터와 동일하게 사용가능!
pa(address) : 0x0
pb(address) : 0x600002b08000
자원을 해제함!
```

이동 생성자는 가능하기 때문에, `std::move()` 함수로 우측값 래퍼런스를 전달하면서 이동 생성자를 호출하고 소유권이 된다. 이전 되기 전에 `pa ` 는` pa.get()`함수를 호출하면 주소값이  0 이 나오면서 소유권이 이전 되는걸 확인할 수 있다. 

* `get` 함수는 `unique_ptr` 이 소유하고 있는 객체에 주소값을 반환한다.

정리하면,

- `unique_ptr` 은 어떤 객체의 유일한 소유권을 나타내는 포인터 이며, `unique_ptr` 가 소멸될 때, 가리키던 객체 역시 소멸된다.
- 만약에 다른 함수에서 `unique_ptr` 가 소유한 객체에 일시적으로 접근하고 싶다면, [get](https://modoocode.com/191) 을 통해 해당 객체의 포인터를 전달하면 된다.
- 만약에 소유권을 이동하고자 한다면, `unique_ptr` 를 [move](https://modoocode.com/301) 하면 된다





