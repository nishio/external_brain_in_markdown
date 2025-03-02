
手元からS3へのsyncの際、--deleteをつけなければ、手元で消えていてもS3上のデータは消されない
- [sync — AWS CLI 1.16.266 Command Reference](https://docs.aws.amazon.com/cli/latest/reference/s3/sync.html)

--exaxt-timestampが付いていない場合、ファイルサイズが同じファイルは変更されていないとみなされる
