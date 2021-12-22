# 정렬

## 1. sort

일반적인 정렬 함수, 반복자는 반드시 임의접근 반복자(RandomAccessIterator) 타입을 만족해야한다.

```c++
template <typename Iter, typename Pred>
std::sort(Iter begin, Iter end, Pred pred)
```

`pred` 는 '특정한 조건'을 받는다. **함수 객체(Functor)** 로 전달하면 된다.

평균적으로 *O*(*N*log*N*) 으로 실행된다.





