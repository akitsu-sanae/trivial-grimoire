## Boost.Variant
複数の型の和型を実現する

### 一番簡単な使い方
一番はじめに指定した型がデフォルトになる.  
```cpp
boost::variant<int, std::string> v; // int(0)
```

文字列型も代入できる  
```cpp
v = "hello";
```
`std::string`と同様にstreamingもできる
```cpp
std::cout << v; // hello
```
格納されている値を取り出すには`boost:get<T>`を使う
```cpp
// hello world
std::string hello_world = boost::get<std::string>(v) + "world"
```
どの型の値が格納されているか分からない時は以下のようにする
```cp
auto some_func(boost::variant<int, std::string> const& v)
if (int* pi = boost::get<int>(&v))
    return some_int_func(*pi);  // intが格納されている時の処理
else if (std::string* pstr = boost::get<std::string>(&v))
    return some_str_func(*pstr);// std::stringが格納されている時の処理
```
もしくはこういう風にもできる
```cpp
class some_func_visitor
    : public boost::static_visitor<>
{
    auto operator()(int & i) const {
        // some func
    }
    auto operator()(std::string & str) const {
        // some func
    }
};

boost::apply_visitor(some_func_visitor(), v);
```
今回`int`と`std::string`で処理を分けたが, ほぼ同じ処理の時は`template`を使える
