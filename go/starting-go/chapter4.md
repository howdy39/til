# Chapter 4　参照型
「Slice」「map」「channel」の3つが定義されている

組み込み関数makeを使ってスライス、マップ、チャネルを作る。

## スライス
いわゆる可変長配列

```
var s []int
s = make([]int, 5) // 要素数と容量が5
```

## len
長さを取得する関数

```
var s []int
s = make([]int, 5) // 要素数と容量が5

fmt.Println(len(s)) // => 5
```

## cap
容量を取得する関数  
`capacity`（容量）の略

```
var s []int
s = make([]int, 5, 10) // 要素数が5容量が10
fmt.Printf("%#v\n", s) // => []int{0, 0, 0, 0, 0}

// len
fmt.Println(len(s)) // => 5
// cap
fmt.Println(cap(s)) // => 10
fmt.Println(s[9]) // => 0
```
  
