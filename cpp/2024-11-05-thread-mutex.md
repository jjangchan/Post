## 쓰레드(Thread)

- CPU 코어 안에서 돌아가는 프로그램 단위를 쓰레드(Thread) 라고 한다. 
- 하나의 프로세스 안에 여러개의 쓰레드가 돌아가는 프로그램을 멀티 쓰레드(multithread) 프로그램이라고 한다.
- 쓰레드와 프로세스의 차이점은 메모리 공유다. 프로세스 내 쓰레드들은 메모리를 공유 하고 있지만, 각기 다른 프로세스들은 메모리를 공유하지 않는다.
- 멀티 코어 환경에서는 쓰레드가 병렬적으로 연산 하므로 연산 효율이 높아진다.
  - 쓰레드가 어떤 CPU코어에 할당 하고 컨텍스트 스위치를 할 지는 운영체제 스케줄링에 따라 달려 있다. 만약, 하나의 CPU 코어의 모든 쓰레드가 할당되면, 쓰레드간의 컨텍스트 스위치가 계속 일어나면서 잦은 문맥전환로 오버헤드가 발생하게 된다.



### 쓰레드 예제

```c++
#include <iostream>
#include <thread>
using std::thread;

void func1() {
  for (int i = 0; i < 10; i++) {
    std::cout << "쓰레드 1 작동중! \n";
  }
}

void func2() {
  for (int i = 0; i < 10; i++) {
    std::cout << "쓰레드 2 작동중! \n";
  }
}

void func3() {
  for (int i = 0; i < 10; i++) {
    std::cout << "쓰레드 3 작동중! \n";
  }
}
int main() {
  thread t1(func1);
  thread t2(func2);
  thread t3(func3);
}
```



## 뮤텍스(Mutex)

### 경쟁 상태 (race condition)

동일한 프로세스 내 쓰레드들은 메모리를 공유하게 되는데, 여기서 동일한 자원을 사용하면서 발생하는 문제점을 경쟁 상태(race condition) 이라고 한다.



### CPU 연산에 의한 쓰레드의 문제점

CPU는 연산할 떄 메모리의 데이터값을 레지스터에 가져온뒤, 빠르게 연산한 후 다시 메모리에 가져다 놓는 식으로 작동한다. 아래에 코드의 어셈블리어를 해석하면,

```c++
int main{
	int count = 0;
	count += 1;
}
```

```assembly
  # rax = *(int**)(rbp-8);
  # -> (rbp-8)의 주소값을 rax에 대입
  mov rax, qword ptr [rbp - 8]
  # ecx = *(int*)rax
  # -> rax의 정수값을 ecx에 대입
  mov ecx, dword ptr [rax]
  # ecx += 1;
  add ecx, 1
  # rax = ecx
  # -> rax에 ecx 값 대입
  mov dword ptr [rax], ecx
```

- `rax` , `rbp` 는 레지스터
- `mov` 는 대입 명령, `word` 는 2바이트, `dword` 는 4바이트, `qword` 는 8바이트
- `[rax]` 는 역참조를 의미



문제는, 하나의 cpu코어에서 2개의 쓰레드가 실행하는 멀티쓰레드의 환경에서 쓰레드간의 컨텍스트 스위칭이 이루어지면서 데이터의 결과값을 뒤덮어서 결과가 계속 달라지는걸 볼수 있다. 아래의 예제처럼,



![td1](../img/td1.PNG)

- 쓰레드1에서 `rax`의 값을 `ecx`에 대입하는 과정까지 이루어지고, 쓰레드2로 컨텍스트 스위칭 이 발생했다.
- 쓰레드2는 모든 어셈블리를 수행 했으므로 결과값이 1이 된다. 그리고 다시 쓰레드1로 컨텍스트 스위칭이 발생했다.
- 쓰레드1에서 나머지 연산을 처리하기 위해 `rax`에 `ecx`에 1이 올라간 값을 대입 했다. 다시 결과값이 1이 들어가면서 값을 덮어버린다.

<hr/>

참고로 각 쓰레드는 메모리를 공유할 지언정, 레지스터는 공유하지 않습니다. 따라서 각 쓰레드 별로 고유의 레지스터들을 가지고 있다고 생각하셔도 됩니다. 즉, 쓰레드 1 의 ecx 와 쓰레드 2 의 ecx 는 서로 다르다고 보시면 됩니다.

<hr/>





> 출처
>
> https://modoocode.com/135