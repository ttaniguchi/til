# rbenv
## インストール方法
- rbenvとruby-buildを入れる
```sh
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
cd  ~/.rbenv/plugins/ruby-build
sudo ./install.sh # rootで叩く必要がある
```

- .bashrcに追記
```sh
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"

```

## ディレクトリごとのrubyバージョン固定
- .ruby-version
```
2.4.2
```
