## 함수의 오버로딩 이란?

이름이 동일한 함수에 인자를 다르게 해서 과부하를 줍니다. 



## static 이란?

static 변수 또는 함수를 클래스 내부에 설정하면, 특정 객체에 종속되지 않고 클래스에 종속하게 된다. 한마디로 같은 클래스 내에서 static은 공유가 가능합니다.



## const 이란?

const은 읽기전용입니다. const 변수는 수정이 불가능합니다.

const 함수는 멤버변수의 수정이 불가능하고 상수함수만 호출할 수 있습니다. 하지만 mutable를 활용해서 멤버변수를 접근 가능하게 할 수도 있습니다.



## 생성자 리스트의 장점 

생성자리스트는 생성과 초기화를 동시에 합니다. 이에 따른 장점은 

1. 만약 type이 클래스이면 생성자리스트는 복사생성자만 호출하고 생성자리스트를 쓰지 않았으면 생성자를 호출하고 대입연산자를 호출한다. 따라서 전자가 더 효율적인 작업입니다.
2. 상수와 레퍼런스들은 모두 생성과 동시게 초기화가 되어야해서 무조건 초기화 리스트를 사용해야한다.



## 레퍼런스 인자를 사용하는 이유?

값을 받지 않고 주소값을 받습니다. 

여기서 불필요한 복사가 일어나지 않습니다. 만약  인자가 레퍼런스가 아닌데 큰 데이터가 들어있는 컨테이너, 구조체, 클래스 이면 안에 있는 element를 다 복사하니깐 속도도 느리고 비효율적 입니다.



## 깊은 복사 or 얕은 복사

디볼트 복사 생성자 or 대입 연산자는 대입만 해주는 __얕은 복사(shallow copy)__ 일어납니다. 여기서 동적으로 할당된 메모리를 동시 참조하다가 a에서 delete를 해주고 b에서 delete된 메모리를 호출하면 런타임 에러가 발생합니다. 이러한 문제점을 해결하기 위해서는 따로 메모리에 동적 할당해서 복사하는 방법 즉 깊은 복사를 해야 합니다.



## malloc() 과 new의 차이

malloc()은 함수이고 , new는 연산자입니다. 큰 차이점은 생성자 유무 입니다. malloc()은 시스템 함수로서 함수 안에서 메모리를 할당하지만 new는 연산자로 바로 메모리를 할당하는게 아니라 생성자를 호출하여 메모리를 할당합니다. 그러므로 생성 시 초기화가 가능한 장점이 있습니다.



## 객체지향언어 vs 절차지향언어

절차지향언어는 순차적 실행, 컴퓨터의 처리구조와 유사해 객체지향보다 빠른 처리가능, 계산중심언어, 함수가 중심이 되고 데이터는 보조기능입니다.

객체지향언어는 실제 세계를 모델링 또한 추상화, 캡슐화, 상속, 다형성의 특징이 있습니다

- 추상화 : 수행과정이 비슷한 개념으로 묶어 정의(선언)하는 것을 추상화라고 합니다.
- 캡슐화 : 프로퍼티(변수)와 메소드(함수)가 하나의 캡슐 안에 묶인 특성을 말합니다.
- 상속성 : 하나의 클래스가 가지고 있는 특징을 그대로 다른 클래스에게 물려줍니다.
- 다형성 : 하나의 객체가 여러 형태를 가질 수 있음을 의미합니다. 대표적으로 오버라이딩과 오버로딩이 있습니다.



## 프로세스 & 스레드

프로세스 : 프로그램을 메모리 상에서 실행중인 작업 

스레드 : 프로세스 안에서 실행되는 여러 흐름 단위



프로세스는 각각 별도의 주소공간 할당(독립적)

- code : 코드 자체를 구성하는 메모리 영역(프로그램 명령)
- Data : 전역변수, static, 배열등
  - 초기화 된 데이터는 data영역에 저장
  - 초기화 되지 않은 데이터는 bss 영역에 저장
- Heep : 동적 할당시 사용(new(), malloc()) 등
- Stack : 지역변수, 매개변수, 리턴값 (임시 메모리 영역)



스레드는 Stack만 따로 할당 받고 나머지 영역은 서로 공유 

하나의 프로세스가 생성될 때, 기본적으로 하나의 스레드 같이 생성

**프로세스는 자신만의 고유 공간과 자원을 할당받아 사용**하는데 반해, **스레드는 다른 스레드와 공간, 자원을 공유하면서 사용**하는 차이가 존재함



## c++ 4가지 캐스팅

- `static_cast` : 우리가 흔히 생각하는, 언어적 차원에서 지원하는 일반적인 타입 변환
- `const_cast` : 객체의 상수성(const) 를 없애는 타입 변환. 쉽게 말해 `const int` 가 `int` 로 바뀐다.
- `dynamic_cast` : 파생 클래스 사이에서의 다운 캐스팅 (→ 정확한 의미는 나중에 다시 배울 것입니다)
- `reinterpret_cast` : 위험을 감수하고 하는 캐스팅으로 서로 관련이 없는 포인터들 사이의 캐스팅 등



## 소멸자의 virtual 키워드

기반 클래스의 가리키는 파생 클래스 `a` 가 동적으로 메모리가 할당 되어 있는 상태에서  `a` 가 `delete` 될 때 소멸자에 `virtual` 키워드를 명시하지 않으므로 소멸자는 정적바인딩 되어 있는 상태이여서 컴파일 단계에서 형이 기반클래스를 이므로 기반클래스에 소멸자만 호출 한다 따라서 메모리 누수가 발생한다. 소멸자의 `virtual` 키워드를 명시하면 동적바인딩 되여서 소멸자를 호출시 런타임 단계에서 가상함수테이블를 거치면서 기반클래스의 소멸자를 찾아서 호출시켜준다.



## 스마트포인터의 존재

똑똑한 포인터의 역할을 하는 객체 입니다. 적은버그, 자동청소, 자동초기화, 댕글링포인터 등에 대한 이점이 있습니다. std::unique_ptr은 있으면 소유권을 독접하기 때문에 복사생성이 안됩니다. 그러나 이동(소유권이전)은 가능합니다.



## 동기화(mutex, atomic) 을 사용하는 이유?

CPU에서 연산을 할 떄 레지스터에 연산을 합니다. 예를들어 a 랑 b 쓰레드가 있습니다.

a가 역참조된 변수에 레지스터에 `add`연산자로 1을 더하기전에 b가 먼저 `add`연산자로 1을 더했습니다. 하지만 a는 `add`를 하기 전 상황이므로 `add`를 하면 변수의 결과값을 뒤덮어서  +1이라는 계산을 한번 누락시키게 됩니다. 



![iostream1](../img/tread1.PNG)



## Intrusive set 사용이유

`std::set`은 각 노드를 별도로 동적 할당하기 때문에 삽입/삭제 시 allocator 비용이 발생하고 노드와 객체가 분리되어 있어 메모리 접근 시 캐시 효율이 떨어질 수 있다.

```c++
std::set
    │
    ├── new Node
    │      ├── left
    │      ├── right
    │      ├── parent
    │      └── Websocket
    │
    ├── new Node
    ├── new Node
    └── ...
```



 반면 `boost::intrusive::set`은 객체 내부의 `set_member_hook`이 RB Tree 노드 역할을 하므로 별도의 노드 할당이 필요 없고, 노드와 객체가 동일한 메모리 블록에 존재해 메모리 지역성이 더 좋아질 수 있습니다. 따라서 저지연이 중요한 서버나 HFT 환경에서 자주 사용된다.

 ```c++
Websocket 객체

+-----------------------+
| hook (RBTree Node)    |
+-----------------------+
| socket                |
| id                    |
| ...                   |
+-----------------------+

class Websocket
{
    set_member_hook<> hook; // --> RBTree Node... 1 set by 1 hook
    ...
};
 ```



## lock-free queue 를 사용해야하는 이유

현재 내가 구현한 암호화폐거래소의 큰 문제점은 병목현상이 발생하면 `Boost.Asio` 가  `kernel Socket Buffer` 에 계속 쌓아놓는걸 빠르게 처리하지 못해서 지연이 발생한다.

```markdown
Exchange
    │
    ▼
Kernel Socket Buffer
```

 `kernel Socket Buffer` 가 꽉 차면 TCP Flow Control이 발생하거나 최악의 경우 상대방이 연결을 끊을 수도 있다.

병목현상이 최대한 줄이는 방식으로 설계를 해야하는데 지금 코드는 **같은 WebSocket에서는 항상 하나의 read만 outstanding** 를 하지 않는다.

```c++
void start_read()
{
    w_socket.async_read(
        buffer,
        std::bind(&Websocket::ws_on_read,
                  shared_from_this(),
                  _1, _2));
}

void ws_on_read(error_code ec, std::size_t bytes)
{
    // 1. JSON 파싱

    // 2. 전략 실행
    strategy->on_tick(...);

    // 3. 다음 read 등록
    start_read();
}
```

29ms 동안 여러개의 틱이  도착한다면...

```markdown
t = 0ms    Tick1 도착
t = 1ms    Tick2 도착
t = 2ms    Tick3 도착
.
.
.
.
t = 29ms   TickN 도착
```

2번 전략 실행 함수 `on_tick()` 에서 30ms 발생하면 N개의 Tick 신호가 버퍼에 쌓이면서 수신 처리량을 견더내지 못해 지연되게 된다. 

해결 방법은 네트워크 I/O 와 전략 로직을 분리해서 `SPSC lock-free queue` 로 관리해야한다. 

```
WebSocket Thread
----------------------------
async_read
    │
JSON Parse
    │
Lock-Free Queue에 Push
    │
async_read() 즉시 재등록
----------------------------

Strategy Thread
----------------------------
Queue Pop
    │
Indicator 계산
    │
Order 생성
----------------------------
```

> "초기에는 `async_read` 콜백에서 바로 전략을 수행했는데, 전략 처리 시간이 길어지면 다음 `async_read` 등록이 늦어져 OS 소켓 버퍼에 데이터가 누적되고, 이후 틱이 한꺼번에 처리되는 현상을 경험했습니다. 이를 통해 네트워크 I/O와 전략 처리를 분리해야 한다는 점을 이해했습니다."

### 어떻게 Lock-free queue 를 설계해야하는가

단일 생성자 쓰레드(네트워크) 는 항상 틱 신호를 `push` 한다. 단일 소비자 쓰레드(전략) 는 항상 틱 신호를 `pop` 한다. 이점을 이용해서 SPSC lock-free queue 를 구현해보자.

```c++
//
// Created by jjangchan on 2026/07/27.
//

#ifndef MAIN_CPP_MYSPSCLOCKFREEQUEUE_H
#define MAIN_CPP_MYSPSCLOCKFREEQUEUE_H
#include <iostream>
#include <array>
#include <atomic>
#include <algorithm>

template<typename T, std::size_t size>
class SPSCLockFreeQueue{
    static_assert(
            size != 0 && (size & (size - 1)) == 0,
            "Size must be a power of two."
    );
private:
    std::array<T, size> q;
    alignas(64) std::atomic<std::size_t> head{0};
    alignas(64) std::atomic<std::size_t> tail{0};

public:
    SPSCLockFreeQueue(){}

    explicit SPSCLockFreeQueue(const std::array<T, size>& buffer){
        for(int i = 0; i < buffer.size(); i++) q[i] = buffer[i];
    }

    explicit SPSCLockFreeQueue(const SPSCLockFreeQueue& q) = delete;

public:
    bool push(T&& data){
        std::size_t new_tail = tail.load(std::memory_order_relaxed);

        std::size_t next_tail = (new_tail+1) & (size-1);
        if(next_tail == head.load(std::memory_order_acquire))
            return false; // 큐 꽉참...

        q[new_tail] = std::move(data);

        tail.store(next_tail, std::memory_order_release);

        return true;
    }

    bool pop(T& data){
        std::size_t new_head = head.load(std::memory_order_relaxed);

        if(new_head == tail.load(std::memory_order_acquire))
            return false; // Empty...

        data = std::move(q[new_head]);

        head.store((new_head+1) & (size-1),
                   std::memory_order_release);

        return true;

    }

};

#endif //MAIN_CPP_MYSPSCLOCKFREEQUEUE_H

```

#### 1. 쓰기는 생성자-소비자 끼리 중복되지 않고 1개의 연산으로 원자적 처리

 ```c++
std::atomic<size_t> tail;
std::atomic<size_t> head;
 ```

- Producer가 `tail`을 **쓰기(write)** 연산만 사용

```c++
tail.store(next_tail, std::memory_order_release);
```

- Consumer가 `head`를 **쓰기(write)**  연산만 사용 

 ``` c++
head.store((new_head+1) & (size-1), std::memory_order_release);
 ```

- Producer가 `head`를 **읽기(read)** 연산만 사용

 ``` c++
if(next_tail == head.load(std::memory_order_acquire))
	return false; // 큐 꽉참...
 ```

- Consumer가 `tail`을 **읽기(read)** 연산만 사용

 ```c++
if(new_head == tail.load(std::memory_order_acquire))
	return false; // Empty...
 ```



#### 2. 거짓공유(False Sharing) 방지

   생성자 , 소비자 쓰레드가 cpu 각 코어 에 배치된다면..

```
Core 0                     Core 1

Producer                   Consumer

push()                     pop()

push()                     pop()

push()                     pop()
```

두 스레드가 **진짜 동시에** 실행

- Producer는 계속 데이터를 생성
- Consumer는 계속 데이터를 소비

하면서 Lock-Free Queue의 장점을 최대한 활용할 수 있다.

문제점은 각 코어마다  64byte `Caching line` 를 통째로 가져와서 읽으므로.. 만약 `tail` 또는 `read` 값이 변경된다면 MESI 프로토콜에 의하여 캐시 일관성 비용이 든다.

>MESI 프로토콜 4가지 상태
>
>- **Modified (M)**: 데이터가 수정된 상태이며, 메인 메모리와 값이 다릅니다. 이 캐시만 최신 값을 가집니다.
>- **Exclusive (E)**: 데이터가 이 캐시에만 존재하며, 메인 메모리 값과 완벽히 일치합니다.
>- **Shared (S)**: 여러 코어의 캐시가 이 데이터를 똑같이 가지고 있으며, 메인 메모리도 최신 상태입니다.
>- **Invalid (I)**: 캐시 라인에 유효한 데이터가 들어있지 않아 사용할 수 없는 상태입니다. 
>
>예시)
>
>CPU1이 메모리 A를 읽음 -> 캐시에 없음 -> 메인 메모리에서 읽어옴 -> 상태는 E
>
>CPU2도 A를 읽음 -> CPU1의 A는 S, CPU2의 A도 S
>
>CPU2가 A를 씀 -> CPU1의 A는 I, CPU2의 A는 M
>
>CPU1이 다시 A를 읽음 -> CPU2로부터 snooping통해 data 받음 -> 둘다 S

 이러한 문제점을 해결하기 위해서는 c++ `alignas(64)` 로 캐싱라인에 할당한 변수만 보관하고 나머지는 `padding` 시킨다

```c++
alignas(64) std::atomic<std::size_t> head{0};
alignas(64) std::atomic<std::size_t> tail{0};

0x1000, core 0  Caching line (64Byte)
+---------------------------+
| head | padding....        |
+---------------------------+

0x1040, core 1  Caching line (64Byte)
+---------------------------+
| tail | padding....        |
+---------------------------+
      (64Byte)
```

하지만 alignas(64)을 남발하면 안된다.  Cache Line Padding의 Trade-off 문제가 있다.

L1 캐시 크기는 코어당 보통 **32KB~128KB** 으로 되어있다. padding 된 Cash Line을 L1 캐시에 저장할 수 있는 단위가 작어지면서 오히려 Cache Miss가 증가할 수도 있다. 따라서 

① 같이 사용하는 데이터 같은 Cache Line에 묶고

② 서로 다른 코어가 수정하는 데이터 분리해서 False Sharing을 막아야 한다.



#### 3. 생성자-소비자 동기화(memory order)

- **Release**: *이전의 메모리 접근*이 Release 뒤로 넘어가 다른 스레드에서 관측되지 않도록 보장.

```c++
std::size_t new_tail = tail.load(std::memory_order_relaxed);

q[new_tail] = std::move(data);

tail.store(next_tail, std::memory_order_release); // store -> load 순으로 관측되지 않도록 보장.
```

- **Acquire**: *이후의 메모리 접근*이 Acquire 앞으로 당겨져 관측되지 않도록 보장.

```c++
Producer

buffer 작성 완료

↓

tail.store(release)

======================

tail.load(acquire)

↓

Consumer

buffer 읽기
```

이 순서가 강제됩니다.

즉

**Consumer는 `tail`을 확인하기 전에는 `buffer`를 읽을 수 없다.

그래서

- Producer가 데이터를 다 써놓고
- "준비 완료"(`tail.store(release)`)를 알린 뒤에만
- Consumer가 데이터를 읽는다.

만약 관측이 보장되지 않고 재배치 된다면 이슈는,

* **미리 읽어 둔 오래된 값이나 미완성 데이터를 사용**하게 된다.

즉 **다른 스레드가 관측하는 순서(visibility)를 보장**하는 것이 핵심이다.



#### 4. ring buffer(비트연산)

`tail`, `head` 에 인덱스를 증가시키는 방법으로 지정 사이즈가 초과되면 다시 0 으로 돌아간다.

```c++
(new_tail+1) & (size-1)

taile = 7, size = 8   

  1000 --> 7 + 1
& 0111 --> 8 - 1
  0000 --> 0 인덱스로 순환
```

















