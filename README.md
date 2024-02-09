# 使い方

Zenn の記事を Qiita の記事に変換する

Zenn記法で記事を書き、articlesフォルダーに入れる

以下のコマンドでqiitaの記事を生成

./node_modules/.bin/ts-node scripts/ztoq.ts ./articles/記事ファイル名 ./qiita/public/

qiita/publicにQiitaの記事が生成する

qiita_articles で npx qiita new 記事名 で記事を生成し（idの生成のために必要）、中身を貼り付ける