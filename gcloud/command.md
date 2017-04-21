# アプリケーションのデプロイ(app deploy)
```
gcloud app deploy [DEPLOYMENTS]
```

```
gcloud app deploy app.yaml
```

## 複数サービスある場合
```
gcloud app deploy main/app.yaml service1/app.yaml service2/app.yaml
```

## デプロイ時にトラフィックを割り当てない
```
--no-promote
```

## cronのデプロイ
`gcloud app deploy cron.yaml`


# データストアのインデックス作成(datastore create-indexes)
```
gcloud datastore create-indexes index.yaml
```
