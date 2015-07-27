## Aggregates
これはN4140を参考にして書いている.  
Aggregate型であれば{}を使ってメンバをAggregate初期化できる.  

### Aggregateの定義
配列型であるか, 次の条件を満たせばAggregate型である.  
* ユーザー定義のコンストラクタを持たない
* private/protectedな非静的メンバを持たない
* 基底クラスを持たない（つまり継承してない）
* 仮想関数を持たない




