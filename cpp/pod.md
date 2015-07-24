## PODについて
N4140の9 Classesを参考にしました.
### POD classとは
POD structもしくはPOD unionのことである.  

### POD structとは
以下の条件をすべて満たせばPOD structである.  
* union classではない
* trivial classである
* standard-layout classである
* 全ての非静的メンバがPOD classかその配列である

### POD unionとは
以下の条件をすべて満たせばPOD unionである.  
* union classである
* trivial classである
* standard-layout classである
* 全ての非静的メンバがPOD classかその配列である

### trivial classとは
以下の条件をすべて満たせばtrivial classである.  
* デフォルトコンストラクタを持つ
* trivialでないデフォルトコンストラクタを持たない
* trivially copyableである

### trivially copyableとは
以下の条件をすべて満たせばtrivially copyableである.  
* trivialでないコピーコンストラクタを持たない
* trivialでないムーブコンストラクタを持たない
* trivialでないコピー代入演算子を持たない
* trivialでないムーブ代入演算子を持たない
* trivialなデストラクタを持つ

### standard-layout classとは
n4140を参照している.  
n4296では定義が変わっているので注意すること.  
以下の条件をすべて満たせばstandard-layoutである.  
* 仮想関数や仮想基底クラスを持たない
* 全ての非静的メンバのアクセス指定子が同じである
* 全ての基底クラスがstandard-layout classである
* そのクラスとそのクラスの派生元のすべてのクラスの内, 非静的メンバを持っているのは高々一つである
* 一番目の非静的メンバと同じ型を基底クラスとして持たない
* 全ての非静的メンバがstandard-layout classかその配列か参照である

