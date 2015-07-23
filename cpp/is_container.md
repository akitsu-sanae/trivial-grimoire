### テンプレート引数がコンテナクラスか判断する
N4296 §23.2.1にContainers requirementsとして要件が表にまとめられているので, それを参考にすればいい.  
要求を網羅しているわけではないが, 悪意がない限り以下のようにすれば十分だと思う.  
```cpp
template<
    typename T,
    typename = typename T::value_type,
    typename = typename T::reference,
    typename = typename T::const_reference,
    typename = typename T::iterator,
    typename = typename T::const_iterator,
    typename = typename T::difference_type,
    typename = T::size_type>
void test(T const& t) {
    std::cout << "container type" << std::endl;
}
```

