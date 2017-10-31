# Docker基本操作
## ダウンロード
- https://docs.docker.com/docker-for-mac/install/

## イメージ操作
```sh
docker images     // 一覧
docker pull nginx // 追加
docker rmi nginx  // 削除
```

## コンテナ操作
```
docker run -d -p 80:80 --name webserver nginx // 起動
docker container ls -a              // 一覧
docker exec -it webserver /bin/bash // コンテナに入る
docker container stop webserver     // 停止
docker container rm webserver       // 削除
```
