# Chapter 3　言語の基本

## コメント
`//`で単行コメント

`/* */`で複数行コメント

複数行コメントの中に

## セミコロン
言語的にはセミコロンが自動で入れられている形。

明示的に使用する局面はほとんどない。

## 定義済み識別子
型（bool, byte, int etc）・定数（true, false, iota）・ゼロ値（nil）・関数(append, cap, close, copy etc)

Goの特徴として定義済みであっても変数や関数名として使えるが、混乱の元なので使用を避ける。

## fmtパッケージ
`fmt.printXXX`は標準出力だが、`print`,`println`は標準エラー出力という違いがある。

```
fmt.Println("Hello, Golang!")    // => Hello, Golang!
fmt.Println("Hello,", "Golang!") // => Hello, Golang!

fmt.Printf("10進数=%d 2進数=%b 8進数=%o 16進数=%x\n", 10, 10, 10, 10) // => 10進数=10 2進数=1010 8進数=12 16進数=a

fmt.Printf("数値=%v 文字列=%v 配列=%v\n", 10, "文字列", [...]string{"hoge", "piyo", "fuga"})    // => 数値=10 文字列=文字列 配列=[hoge piyo fuga]
fmt.Printf("数値=%#v 文字列=%#v 配列=%#v\n", 10, "文字列", [...]string{"hoge", "piyo", "fuga"}) // => 数値=10 文字列="文字列" 配列=[3]string{"hoge", "piyo", "fuga"}
fmt.Printf("数値=%T 文字列=%T 配列=%T\n", 10, "文字列", [...]string{"hoge", "piyo", "fuga"})    // => 数値=int 文字列=string 配列=[3]string

print("Hello, World!\n") // => Hello, World!
println("Hello, World!") // => Hello, World!
```

## 変数
以下の３種類の型がある

- 値型
- 参照型（スライス・マップ・チャネル）
- ポインタ型

## 明示的な変数宣言
```
// １つだけ
var n int

// 複数
var x, y, z int

// 複数の型を一括で
var (
    key   int
    value string
)
```

## 暗黙的な変数宣言

```
i := 1
i := 2 // :=はあくまで定義なので2度目はエラーになる no new variables on left side of :=
```

## パッケージ変数
グローバル変数はないがパッケージ内の変数はある。

```
package main

var packageVariable = "package変数です"
// packageVariable := "package変数です" // これはエラー暗黙的な宣言は使えない

func main() {
	fmt.Printf("パッケージ変数=%#v", packageVariable)
}
```

## 真偽値型
`bool`

## 整数型
符号付き整数は`int8`, `int16`, `int32`, `int64`

符号なし整数は`uint8`, `uint16`, `uint32`, `uint64`

実装に依存する整数型は`int`, `uint`

リテラルは`int`になる

## 浮動小数点型
`float32`, `float64`

リテラルは`float64`になる

## 複素数型
`complex64`, `complex128`

基本的にリテラルで表現する（varはできない模様）

`c128 := 1.0 + 3i`

リテラルは`complex128`になる

## ルーン型
`rune`

Unicodeエンドポイントをあらわす整数型。`int32`のエイリアス。

## 文字列型
`string`

## RAW文字列リテラル   
```
`
１行目
２行目
`
```

## 配列型
`[5]int{}`や`[5]int{1, 2, 3, 4}`のように宣言する
明示的な初期値が与えられない場合は方にとってのゼロをあらわす値で初期化される。

`int`なら`0`

`string`なら`""`

`bool`なら`false`

## interface{}型
あらゆる型と互換性がある型

+などoperatorを使うことはできない。

## 演算子
省略

## 関数

```
func [関数名]([引数の定義]) [戻り値の型] {
    [関数の本体]
}
```

## 引数の型の省略
同じ型の場合まとめることが可能。

`func plus(x int, y int)`

↓

`func plus(x, y int)`

## 複数の値を返すことが可能

`func div(a, b int) (int, int) {`

## 戻り値の破棄

`a, _ = div(10, 3)`

## 戻り値の省略

```
func doSomething() (x, y int) {
	y = 10
	return
}

// これは以下と同じ

func doSomething() (int, int) {
	var x, y int
	y = 10
	return x, y
}
```

## 無名関数

```
f := func(x, y int) int { return x + y }
fmt.Printf("%T %#v\n", f, f(2, 3)) // => func(int, int) int 5
```

## 即時関数

```
fmt.Printf("%#v\n", func(x, y int) int { return x + y }(1, 3)) // => 4
```

## 関数を返す関数

```
func main() {
	returnFunc()() // I'm a function.
}

func returnFunc() func() {
	return func() {
		fmt.Println("I'm a function.")
	}
}
```

## 定数
`const`

## 定数の省略
値の省略が可能（直前の定数が流れて設定される）

```
const (
	X = 10
	Y // 10になる
	Z = 100
)
```

## 定数の式
式を定数に入れることが出来る

```
const (
	XYZ = X + Y + Z
)
```

## iota
golangには列挙がないがそれに近い役割

```
const (
	A = iota // => 0
	B = iota // => 1
	C = iota // => 2
)
```

## スコープ
大きい単位から以下の順、「パッケージ」「ファイル」「関数」「ブロック」「制御構文」

## パッケージ変数

- 大文字から始まるパッケージ変数は他のパッケージから参照可能
- 小文字から始まるパッケージ変数はパッケージ内からのみ参照可能

## ファイルのスコープ
importはファイル単位。同一パッケージの他のファイルには影響を与えない。

## ブロックスコープ
同じ変数名でもブロックが深くなれば再定義可能

```
a := "hoge"
{
	a := "piyo"
	fmt.Printf("%#v \n", a) // => "piyo"
}
fmt.Printf("%#v \n", a) // => "hoge"
```

## for
golangにはwhileはない。breakやcontinueはある。

```
// while
for {}
for i < 100 {}
```

```
// continue break
for i := 0; i < 20; i++ {
	if i < 10 {
		fmt.Printf("continue:%d\n", i)
		continue
	} else {
		fmt.Printf("break:%d\n", i)
		break
	}
}
```

## range
key,valueを取り出すのに使う。

```
fruits := [...]string{"Apple", "Banana", "Cherry"}
for i, s := range fruits {
	fmt.Printf("i:%d s:%s\n", i, s)
}
```

## switch
デフォルトでbreakがかかったような状態。  
※次のcaseにも通したい場合はfallthroghをいれる。

```
switch n := 3 {
case 1, 2:
	fmt.Println("1 or 2")
case 3, 4:
	fmt.Println("3 or 4")
default:
	fmt.Println("unkhown")
}
```

## panic / recover
panicは基本的には使わない。処理続行不能レベルで使う。  
recoverはdeferと組み合わせて使用する。

```
// recover
defer func() {
	if x := recover(); x != nil {
		fmt.Println("reocver1")
	}
}()
defer func() {
	if x := recover(); x != nil {
		fmt.Println("reocver2") // こっちが呼ばれる
	}
}()

// panic
panic("runtime error")
// fmt.Println("ここにはこない")
```