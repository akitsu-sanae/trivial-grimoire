## iteratorについて
これはN4140の24.2を参考にして書いている

### Iteratorの要求
以下の条件をすべて満たせばIteratorである.  
対象の型Xとその変数rについて
* XはCopyConstructibleである
* XはCopyAssignableである
* XはDestructibleである
* Xの左辺値はswappableである(swappableの定義は後々まとめるつもり)
* *rは参照を返す（ここで, rはdereferenceableである）
* ++rはXの左辺値参照を返す

### Iteratorの種類
Iteratorには以下の四種類がある.  
* InputIterator ... 入力用のiterator
* OutputIterator ... 出力用のiterator
* ForwardIterator ... 後ろの要素にのみ移動できるiterator, InputIteratorとOutputIteratorのsuperset
* BindirectionalIterator ... 隣の要素に移動できるiterator, ForwardIteratorのsuperset
* RandomAccessIterator ... 自由に移動できるiterator, BindirectionalIteratorのsuperset

### InputIteratorの要求
以下の条件をすべて満たせばInputiteratorである.  
要素型Tに対する対象の型Xとその変数a, bについて
* XがIteratorの要求を満たす
* XがEqualiyComparableを満たす
* a != bはbool型を返し, その結果は!(a == b)に等しい（pre: aとbについての===は定義されている）
* *aはTに変換可能である（pre: aはdereferenceable, (void)*aと*aは*aと同等, a == bかつaとbについての==が定義されていれば*aは*bと同等である）
* a->mと(*a).mは等しい（pre: aはdereferenceableである）
* ++rはXの左辺値参照を返す（pre: rはdereferenceable, post: rはdereferenceableまたはrはpast-the-end, rの一つ前の値のいずれのコピーもdereferenceableもしくは==が定義されていることを要求されない）
* (void)r++は(void)++rと同等である
* *r++はTに変換可能であり, {T tmp = *r; ++r; return tmp; }と同等の操作である
つまり, Iteratorの要求を満たし, 比較でき, 次の要素に移動でき, 指し示すデータを参照できることである.

### OutputIteratorの要求
以下の条件をすべて満たせば型変数XはOutputIteratorである.  
型Xの変数rについて
* XがIteratorの要求を満たす
* *r = oの結果は使われない（ここで, この操作のあとrがdereferenceableであることは要求されない, post: rはincrementableである）
* ++rはXの左辺値参照を返す（ここで&r==&r++であり, この操作のあとrがdereferenceableであることは要求されない, post: rはincrementableである）
* r++はconst X&に変換でき, {X tmp = r; ++r; return tmp;}と同等の操作である （ここで, この操作のあとrがdereferenceableであることは要求されない, post: rはincrementableである）
* *r++ = oの結果は使われない（ここで, この操作のあとrがdereferenceableであることは要求されない　post: rはincrementableである）

### ForwardIteratorの要求
以下の条件をすべて満たせば型変数XはForwardIteratorである.  
要素型Tに対する型変数Xの値rについて
* XはInputIteratorの要求を満たす
* XはDefaultConstructibleを満たす
* もしXがmutableなiteratorであれば, referenceはTへの参照である
* もしXがconstなiteratorであれば, referenceはconst Tへの参照である
* r++はconst T&に変換可能な型をかえし, {X tmp = r; ++r; return tmp;}と同等の操作である
* *r++はreferenceを返す
* もしaとbが等しいならば, aとbはともにdereferenceableであるか, またはともにdereferenceableでない
* a == bは++a == ++bを暗に示している
* もしaとbが共にdereferenceableならば, a==bであり, この時に限り*aと*bは同じオブジェクトを指す

### BindirectionalIteratorの要求
以下の条件をすべて満たせば型変数XはBindirectionalIteratorである.  
型変数Xの値rについて
* XはForwardIteratorの要求を満たす
* --rはXの左辺値参照を返す (pre: r == ++sとなるようなsが存在する, post: rはdereferenceableである, --(++r) == r, --r == --sはr==sを暗に示している, &r == &--r)
* r--はconst X&に変換可能な方を返し, {X tmp = r; --r; return tmp;}と同等の操作である

### RandomAccessIteratorの要求
以下の条件をすべて満たせば型変数XはRandomAccessIteratorである.  
型変数Xの値rについて
* XはBindirectionalIteratorの要求を満たす
* r += nはX&型を返し
```cpp
difference_type m = n;
if (m >= 0)
    while (m--) ++r;
else
    while (m++) --r;
return r;
```
と同等の操作である
* a + nもしくはn + aはX型を返し, {X tmp = a; return tmp += n;}と同等の操作である （ここでa + n == n + a）
* r -= nはX&型を返し, { return r += -n; }と同等の操作である
* a - nはX型を返し, {X tmp = a; return tmp -= n;}と同等の操作である
* b - aはdifference_type型を返し, return n;と同等の操作である（ここでa + n == bとなるようなdifference_type型のnが存在する, またb == a + (b  - a）である)
* a[n]はreferenceに変換可能な型を返し, *(a + n)と同等の操作である
* a < bは文脈上boolに変換可能な型をかえし, b - a > 0と同等の操作である
* a > bは文脈上boolに変換可能な型をかえし, b < aと同等の操作である
* a >= bは文脈上boolに変換可能な型をかえし, !(a < b)と同等の操作である
* a <= bは文脈上boolに変換可能な型をかえし, !(a > b)と同等の操作である

### 参考
* [iterator traitsについて](iterator_traits.md)


