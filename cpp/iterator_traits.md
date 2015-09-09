## iterator_traitsについて
<iterator>ヘッダにある
```cpp
iterator_traits<Iterator>::difference_type
iterator_traits<Iterator>::value_type
iterator_traits<Iterator>::iterator_category
iterator_traits<Iterator>::reference
iterator_traits<Iterator>::pointer
```
はそれぞれそれらしい型を示すことが期待される.  
OutputIteratorについてはiterator_categoryがOutputIteratorでその他はvoidと定義されていると期待される.  

iterator_traitsは以下のように定義されている.
```cpp
namespace std {
    template<class Iterator> struct iterator_traits {
        using difference_type = typename Iterator::difference_type;
        using value_type = typename Iterator::value_type;
        using pointer = typename Iterator::pointer;
        using reference = typename Iterator::reference;
        using Iterator_category = typename Iterator::Iterator_category;
    };
}
```
また, ポインタ型に対しては以下のように特殊化されている
```cpp
namespace std {
    template<class T> struct iterator_traits<T*> {
        using difference_type = ptrdiff_t;
        using value_type = T;
        using pointer = T*;
        using reference = T&;
        using Iterator_category = random_access_iterator_tag;
    };
}
```
constポインタ型に対しては以下のように特殊化されている
```cpp
namespace std {
    template<class T> struct iterator_traits<const T*> {
        using difference_type = ptrdiff_t;
        using pointer = const T*;
        using reference = const T&;
        using iterator_category = random_access_iterator_tag;
    };
}
```


