---
title: "Astroファイルのimport文をフォーマットするPrettierプラグインを作りました"
emoji: "🧑‍🚀"
type: "tech"
topics: ["prettier", "astro", "npm"]
published: false
---

# はじめに

Astro ファイルの import 文をフォーマットする Prettier プラグインを作りました。
普段、TypeScript ファイルなどの import 文をフォマットするために[prettier-plugin-organize-imports](https://github.com/simonhaenisch/prettier-plugin-organize-imports)という Prettier プラグインを使用しています。Astro ファイルに対しても同様の機能がほしいと思ったのがきっかけで作成しました。

https://github.com/ot07/prettier-plugin-astro-organize-imports

https://www.npmjs.com/package/prettier-plugin-astro-organize-imports

このプラグインを使用すると、以下のように import 文がソートされます。

![](/images/prettier-plugin-astro-organize-imports/demo.gif)

# インストール方法

まずは、依存関係のあるパッケージとともに、プラグインをインストールします。

```shell
npm install -D prettier typescript prettier-plugin-astro-organize-imports
# or
yarn add -D prettier typescript prettier-plugin-astro-organize-imports
# or
pnpm add -D prettier typescript prettier-plugin-astro-organize-imports
```

次に、Prettier の設定ファイルを編集します。ここでは、`.prettierrc`を編集する例を記載します。

```json: .prettierrc
{
  "plugins": ["prettier-plugin-astro-organize-imports"],
  "overrides": [
    {
      "files": "*.astro",
      "options": {
        "parser": "astro"
      }
    }
  ]
}
```

Prettier は公式では Astro ファイルをサポートしていないため、`prettier-plugin-astro-organize-imports`が提供する`astro`パーサーを使用するように設定しています。

これでインストールは完了です。Prettier のフォーマットコマンドを実行すると、Astro ファイルの import 文がフォーマットされるはずです。

:::message alert
`prettier-plugin-astro`などの他の Astro ファイル用プラグインがインストールされている場合、プラグインの自動ロード機能によってエラーが発生する可能性があります。そのような問題を避けるためには、後述の**プラグインの自動ロードを無効にする**設定を行ってください。
:::

# 他の Prettier プラグインとの互換性

他にも、Astro ファイルに対して機能する Prettier プラグインとして、以下のものがあります。

- `prettier-plugin-astro`
- `prettier-plugin-tailwindcss`

これらのプラグインと併用する場合には、以下のような設定が必要です。

- `prettier-plugin-astro-organize-imports`を最後に読み込む
- `pluginSearchDirs`オプションを`false`に設定し、プラグインの自動ロードを無効にする

```json: .prettierrc
{
  "plugins": [
    "prettier-plugin-astro",
    "prettier-plugin-tailwindcss",
    "prettier-plugin-astro-organize-imports" // 最後に読み込む
  ],
  "pluginSearchDirs": false,
  "overrides": [
    {
      "files": "*.astro",
      "options": {
        "parser": "astro"
      }
    }
  ]
}
```

# 参考にした Prettier プラグイン

##### `prettier-plugin-organize-imports`

`.js`, `.jsx`, `.ts`, `.tsx`, `.vue`ファイルの import 文をフォーマットするプラグインです。import 文をフォーマットする処理を実装する上で参考にしました。

https://github.com/simonhaenisch/prettier-plugin-organize-imports

##### `prettier-plugin-tailwindcss`

Tailwind CSS 用のプラグインで、クラスをソートするものです。他の Prettier と互換性を持たせる方法を参考にしました。

https://github.com/tailwindlabs/prettier-plugin-tailwindcss

##### `prettier-plugin-astro`

Astro ファイルをフォーマットする公式プラグインです。

https://github.com/withastro/prettier-plugin-astro

# さいごに

Astro ファイルの import 文をフォーマットする Prettier プラグインである`prettier-plugin-astro-organize-imports`を紹介しました。

Astro を使用して開発している方は、ぜひ試していただけると嬉しいです。

https://github.com/ot07/prettier-plugin-astro-organize-imports
