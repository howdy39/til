# キーについて

## 自動で採番
`datastore.NewKey`でキーを指定しない場合、数値IDがエンティティのキーとして自動的に生成される
```
datastore.NewKey(c, "Employee", "", 0, nil)
```

`datastore.NewIncompleteKey`を使ったほうがわかりやすいので親切。
```
datastore.NewIncompleteKey(c, "Employee", nil)
```
