# Chapter 2　プログラムの構成と実行

## runで実行
`go run hello.go`

## build -o で出力ファイルを指定してビルド。実行ファイルを作る
`go build -o hello hello.go`

`./hello`

## フォーマットにそっていれば`go build`だけでOK
以下の例はzooディレクトリに作っているため`go build`だけで`zoo`という名前で実行ファイルが作られている

`go build`

```
└── zoo
    ├── animals
    │   ├── elephant.go
    │   ├── monkey.go
    │   └── rabbit.go
    ├── main.go
    └── zoo <- 実行ファイル
```

## `go run xxx`はmainパッケージで別ファイルのものは読み込まない
`go run main.go`と叩いても`app.go`は読み込まれない。

`go run main.go app.go`のように書く必要がある。

`go run *.go`でもOKだがテストファイルも入れてしまう。  

`go build && ./zoo`のようにするとテストは除外して実行できる。

ただし`go build`は全てを舐めるので問題ない。

```
└── zoo
    ├── animals
    │   ├── elephant.go
    │   ├── monkey.go
    │   └── rabbit.go
    ├── app.go
    ├── main.go
    └── zoo
```

## パッケージが混ざっているとエラー
１つのディレクトリには１つのパッケージ定義という原則があるので混ざっていると以下のようなエラーになる。

`package main: found packages main (app.go) and foo (foo.go) in /Users/howdy/VscodeProjects/starting-go/zoo
`

## テストのルール
`_test.go`はテストファイルであることをあらわす

テストファイルのうち`Test`で始まる関数がテストの単位となる

## testでテストの実行
`go test ./animals`

おそらくこれのエイリアスみたいなもの

`go test ./animals/*.go `

```
animals/
├── animals_test.go
├── elephant.go
├── monkey.go
└── rabbit.go
```

## -vでテストの詳細を表示
`go test -v`

```
Tatsuyas-MacBook:zoo howdy$ go test -v ./animals/
=== RUN   TestElephantFeed
--- PASS: TestElephantFeed (0.00s)
=== RUN   TestMonkeyFedd
--- PASS: TestMonkeyFedd (0.00s)
=== RUN   TestRabbitFedd
--- PASS: TestRabbitFedd (0.00s)
PASS
ok  	_/Users/howdy/VscodeProjects/starting-go/zoo/animals	0.011s
```