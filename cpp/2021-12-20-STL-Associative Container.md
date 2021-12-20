# 연관 컨테이너(associative container)

키(key) - 값(value) 구조를 가진 컨테이너이다.

- 키의 존재 유무를 알고싶다면  : **셋(set), 멀티셋(multiset)**
- 값의 값을 알고싶다면 : **맵(map) 과 멀티맵(multimap)**

을 사용하면 된다.



# 셋(set)

## 1. 특징

- 원소를 추가할 때는 `insert` 함수를 사용하면 된다. 하지만 `index`를 지정할 수 없다.
- 셋에 원소를 추가하거나 지우는 작업은 **O(logN)**에 처리된다.
- 반복자 타입은 `BidirectionalIterator` 이다. 즉 임의의 원소를 접근할 수 없고 순차적으로 접근해야한다.
- `sort` 된 상태로 원소들이 유지하며 추가된다.
- `find` 함수가 제공되며, 원소가 있는지 없는지 판단해준다. 만약 없으면 `end` 함수를 리턴한다.
- 검색 또한 정렬된 상태를 유지하기 때문에 작업은 **O(longN)** 처리한다.
- 중복된 원소들이 없다.



## 2. 구조

셋은 내부적으로 트리 구조로 구성되어 있다. 트리의 노드들의 특징은 다음과 같다.

- 왼쪽에 오는 모든 노드들은 나보다 작다
- 오른쪽에 있는 모든 노드들은 나보다 크다



![stl2](../img/stl7.JPG)



만약 찾는 값이 **33** 이면 과정은,

1. 루트 노드 : 20 < **33** → 오른쪽으로 이동
2. 30 노드 : 30 < **33** → 오른쪽으로 이동
3. 45 노드 : 45 > **33** → 왼쪽으로 이동
4. 33 노드 : 33 == **33** → 값 발견

이러한 과정으로 노드들을 탐색한다. 따라서 최대 탐색 횟수는 트리의 높이에 비례한다. 노드 **60** 또는 **33** 의 경우에는 총 4번의 비교가 필요하다. 따라서 최대한 모든 노드들을 꽉 채우는것이 중요하다. 예를 들어서



![stl2](../img/stl8.JPG)



이러한 노드는 시퀀스 컨테이너와 검색 속도가 동일한다. 위와 같은 노드 즉, 한쪽으로 아예 치우쳐버린 트리를 균형잡히지 않는 트리(unbalanced tree) 라고 부른다. 실제 셋의 구현을 보면 위와 같은 상황이 발생하지 않도록 앞서 말한 두개의 단순한 규칙보다 더많은 규칙들을 도입해서 트리를 항상 균형 잡히도록 유지하고 있다.



따라서 셋의 구현상 **O(logN)** 으로 원소를 검색할 수 있따는 것이 보장된다.



```c++
#include <iostream>
#include <set>

template <typename T>
std::ostream& operator<<(std::ostream& os, std::set<T> s){
    os << "[ ";
    for(const auto& element : s) os << element << " ";
    os << "]" << std::endl;
    return os;
}

int main() {

    std::set<int> s;
    // 추가는 insert 함수로 인덱스을 지정할 수 없다.
    s.insert(0);
    s.insert(0); // 중복허용x
    // 오름차순으로 정렬되어 있다.
    s.insert(10);
    s.insert(5);
    std::cout << s;
    // output : [ 0 5 10 ]

    // find 함수사용 가능 -> 없으면 end() 리턴한다.
    if(s.find(20) == s.end()) std::cout << "원소 없음" << std::endl;
    else std::cout << "원소 있음" << std::endl;
    // output : 원소 없음

    if(s.find(0) == s.end()) std::cout << "원소 없음" << std::endl;
    else std::cout << "원소 있음" << std::endl;
    // output : 원소 있음


    return 0;
}
```

