# Webのホスティング

## 参考サイト
[FirebaseでWebサイトを無料でサクッと公開してみる](http://qiita.com/Ijoru/items/5b27f1c32df2222514fb)

## プロジェクト作成

## firebaseをインストール
```
npm install -g firebase-tools
```

## login
使用状況の情報収集に協力するか聞かれる。

```
$firebase login
? Allow Firebase to collect anonymous CLI usage information? No
```

認可してポチポチすすめる

## プロジェクトディレクトリに移動

## Firebaseプロジェクトとして登録
```
firebase init
```

DatabaseかHostingが選べるところはHostingを選ぶ

```
? What Firebase project do you want to associate as default
```
プロジェクトとの紐付け。
既に作ったプロジェクトを選択。

他にもSPAにするとか聞かれるので適当に選択。


## デプロイ
```
firebase deploy
```
