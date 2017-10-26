# nginxにてphp-fpm環境構築
## インストール方法

```
sudo yum --enablerepo=remi install nginx php php-fpm php-devel php-cli php-xml php-pgsql php-mbstring php-gd
```

postgresqlを利用していたので、php-pgsqlを追加してあります。

## php-fpm実行ユーザーの変更
vagrantだったので、vagrantユーザーに変更

```
sudo vi /etc/php-fpm.d/www.conf
```

以下を書き換える

```diff
- listen.user = nobady
- listen.group = nobady
+ listen.user = vagrant
+ listen.group = vagrant

- user = apache
- group = apache
+ user = vagrant
+ group = vagrant
```

## nginx.conf設定
- /etc/nginx/conf.d/下に適当なファイルを作成する。
    - 上記はnginx.confにてワイルドカードで取得している。

```nginx
server {
    listen 3001;
    charset utf-8;
    server_name localhost;
    client_max_body_size 100m;

    ## for VirtualBox bug : http://docs.vagrantup.com/v2/synced-folders/virtualbox.html
    sendfile off;

    expires -1;
    include /etc/nginx/mime.types;

    root /home/vagrant/project; # 適宜変更

    location / {
        index  index.html index.htm;
    }
    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

## chkconfigへの登録
やっておくとサーバー起動時にスタートしてくれる。

```bash
sudo chkconfig nginx on
sudo chkconfig php-fpm on
sudo chkconfig --list
```
