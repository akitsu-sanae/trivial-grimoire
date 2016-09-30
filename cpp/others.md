## その他

### これがコンパイルエラーになってへーってなった
```cpp
#include <memory>
struct Hoge {
    auto fuga() { return true; }
};

int main() {
    if (auto&& x=std::make_shared<Hoge>() && x->fuga()) {}
}
```
g++ 7.0だと
```
main.cpp: In function 'int main()':
main.cpp:7:48: error: use of 'x' before deduction of 'auto'
     if (auto&& x = std::make_shared<Hoge>() && x.fuga()) {}
```
と怒られる。  
つまりxの型が推論できる前にxを使用してしまってるので駄目ということらしい  

### ラムダ式でvariadic template

```
[&](auto&& ... args) {
    return f(args ...);
}
```

みたいに出来る。  
今まで知らなかった。  

