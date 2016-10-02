## Recursive Lambda in Rust

参考:  
http://stackoverflow.com/questions/16946888/is-it-possible-to-make-a-recursive-closure-in-rust  
http://smallcultfollowing.com/babysteps/blog/2013/04/30/the-case-of-the-recurring-closure/  

* 外の環境を取り込む必要が無いとき
```
fn main() {
    fn fib(x: i64) -> i64 {
        if x < 2 { 1 }
        else { fib(x-1) + fib(x-2) }
    }
    println!("{}", fib(6));
}
```

* 外の環境を取り込むとき
```
fn main() {
    struct Fib<'s> { f: &'s Fn(&Fib, i64) -> i64 }
    let fib = Fib {
        f: &|fib, x| {
            if x < 2 { 1 }
            else { fib(x-1) + fib(x-2) }
        }
    };
    println!("{}", (fib.f)(&fib, 6));
}
```

