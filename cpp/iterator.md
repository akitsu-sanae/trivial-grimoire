## iteratorについて
これはN4140を参考にして書いている

### Iteratorの要求
以下の条件をすべて満たせばIteratorである.  
対象の型Xとその変数rについて
* Xはコピーコンストラクタを持つ
* Xはコピー代入演算子を持つ
* Xはデストラクタを持つ
* Xの左辺値参照はswappableである(swappableの定義は後々まとめるつもり)
* *rはある型の参照を返す
* ++rはXの左辺値参照を返す

### Iteratorの種類
Iteratorには以下の四種類がある.  
* InputIterator ... 入力用のiterator
* OutputIterator ... 出力用のiterator
* BindirectionalIterator ... 隣の要素に移動できるiterator, InputIteratorとOutputIteratorのsuperset
* RandomAccessIterator ... 自由に移動できるiterator, Bindirectionaliteratorのsuperset

### InputIteratorの要求
以下の条件をすべて満たせばInputiteratorである.  
要素型Tに対する対象の型Xとその変数a, bについて
* XがIteratorの要求を満たす
* XがEqualiyComparableを満たす
* a != bはbool型を返し, その結果は!(a == b)に等しい
* *aはTに変換可能である
* a->mと(*a).mは等しい
* (void)r++
* *r++はTに変換可能である
つまり, Iteratorの要求を満たし, 比較でき, 次の要素に移動でき, 指し示すデータを参照できることである.

