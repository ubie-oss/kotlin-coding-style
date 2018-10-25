# Kotlinコーディングスタイル

あくまでガイドラインです。
あなたは状況に応じて原則を破ることができますが、その判断は慎重に、そしてコメント等でその判断に至った背景や理由を語ってください。

スタイルはktlintに従ってください。
ただし、人間がいくつか気をつけることがあります。

## シンプルに保つ

重要な原則です。
難しいことはしないで、常にシンプルになるよう心がけてください。

例えば、ネストした制御構文は人類には難しすぎるコードです。
副作用の扱いも慎重に。

Kotlinにユニークな機能に関して言えば、publicな拡張関数の導入には注意が必要です。

## テストコードは極めて素直に

テストコードでは、DRYにすることに躍起にならないでください。
同じコードを繰り返してもかまいません。
素直に、愚直に、単純に。まして何かを抽象化するメリットはほぼないでしょう。

* 処理の塊を見つけてもメソッド化する必要はないかもしれません
* リテラルに名前を付ける必要はないかもしれません。何度も同じリテラルを記述しましょう

## 型を明記する

型を明記してください。
ただし、次の場合は例外です。

* ローカル変数の型
* テストコード
* Single-expression functionでなく戻り値の型が`Unit`の関数

## Single-expression function

Single-expression functionは、そのシグネチャから式の開始までを同じ行に書く必要があります。
`=`や式の開始が、シグネチャの次の行から始まる場合はSingle-expression functionの使用を諦めてください。

```kotlin
// OK
fun printHelloWorld(): Unit = println("Hello, world!")

// OK
fun newPerson(
    name: String,
    age: Int
): Person = Person(
    name,
    age
)

// NG
fun findUserByName(name: String): User? =
    userRepository.findUserByName(name)

// OK
fun findUserByName(name: String): User? {
    return userRepository.findUserByName(name)
}
```

## NotNull変換

`!!`は使わずに`requireNotNull`を使用してください。

## lateinitは使用しない

フレームワークの都合上やむを得ない場合を除き、`lateinit`は使用しないでください。

## ブレースは省略しない

制御構文においてブレース（`{}`）は省略しないでください。
ただし、下記の場合を除きます。

* else-if
* `return`, `break`, `continue`, `throw`
