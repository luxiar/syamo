syamo
=====

Gitlabの更新情報(Push、Issue、MergeRequest)をChartworkに通知するサーバです。

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Usage
### herokuに配置
事前に、herokuのアカウントを作成し、`heroku toolbelt`をインストールしてください。

秘密情報を環境変数を設定します。

- CHATWORK_TOKEN:[ChartworkのAPIトークン](http://developer.chatwork.com/ja/)
- GITLAB_URL:gitlab apiのurl(例:https://gitlab.com/api/v3)
- GITLAB_TOKEN:gitlab apiのトークン

```
git clone git@github.com:ledsun/syamo.git
cd syamo
heroku create myapp
heroku config:add CHATWORK_TOKEN=XXX
heroku config:add GITLAB_URL=YYY
heroku config:add GITLAB_TOKEN=ZZZ
git push heroku master
```

※ myappはherokuに作成するアプリケーション名です。好きな名前に変更してください。

### 配置確認
配置に成功したか確認します。

```
cd tools
/bin/bash testHeroku.sh myapp 20003286
```

※ 第一引数にherokuのアプリケーション名を、第二引数チャットルームIDを指定してください。

### Gitlabのwebhook設定
GitlabのProjectのSettingsからwebhooksを登録します。

1. gitlabのプロジェクトを開きます
1. `Setting`を開きます
1. `Web Hooks`を開きます
1. `URL`に http://myapp.herokuapp.com/gitlab/チャットルームID （数字のみ） を入れます
1. `Push events`のチェックを入れます
1. `Add Web Hook`ボタンを押します

## Customize

- テンプレートを変更することで通知内容を変更することが出来ます。
- テンプレートは`template`ディレクトリに入っています。
- テンプレートはmustacheテンプレートです。
- テンプレート名は更新種別[.チャットルームID].mustacheです。
  - 更新種別はissue、merge_request、pushの3種類です。
  - チャットルームIDを指定することで、特定のチャットルームにだけ適用することができます。
- rawプロパティを参照すると全ての情報をJSON形式で表示します。

## Development

bash

```
npm install
export CHATWORK_TOKEN=XXX
export GITLAB_URL=YYY
export GITLAB_TOKEN=ZZZ
npm start
```

fish

```
npm install
env CHATWORK_TOKEN=XXX GITLAB_URL=YYY GITLAB_TOKEN=ZZZ npm start
```

## Test

```
npm test
```

※ 環境依存のためテストは失敗します。

## Why Syamo?
参考にしたアプリケーションの名前をもじってつけました。

https://github.com/astronaughts/chabot

Thank you!
