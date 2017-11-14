# Rails migration
## マイグレーション実行・切り戻し
```sh
bundle exec rake db:migrate
bundle exec rake db:rollback
```

## Revert等によるDBの手動切り戻し
- DBにて変更内容を手動で戻す
- schema_migrationsテーブルからdb/migrateファイルとマッチしないステップのレコードを削除する
