## はじめに
既存のRailsアプリの開発環境にDockerを導入しようとしたところ、bundle installがなかなか上手くいかずに困ったので、その時の対処法について書こうと思います。

今回は、表題の件についての対処法のみ書きますので、既存のRailsアプリにDockerを導入する方法については割愛いたします。

## 環境
- Rails 5.2
- Ruby 2.5.1
- bundler バージョン 2.1.4

## 今回のケース
DockerでRailsの環境を構築する際に、bundlerのバージョンが2.0.1以上だとbundle installに失敗してしまうようです。

こちら、bundle installが上手くいかなかった時のDockerfileになります。

```:Dockerfile
※失敗バージョン

FROM ruby:2.5.1

RUN apt-get update && \
    apt-get install -y mysql-client nodejs vim --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /myapp

WORKDIR /myapp

COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock

RUN gem install bundler
RUN bundle install

COPY . /myapp
```

今回はホストで開発したアプリを、後からコンテナ化した為、コンテナ側にコピーするGemfile.lockには既にホスト側のbundlerのバージョンが記載されていました。
そのバージョンが 2.1.4 だった為、エラーが出てしまったようです。

## 対処法
ver 2.0.1 以上のbundlerを使用する場合、環境変数でbundlerのバージョンを指定する事で、エラーを回避できるようです。

さっそく試してみました。

```:Dockerfile

※成功バージョン

FROM ruby:2.5.1

RUN apt-get update && \
    apt-get install -y mysql-client nodejs vim --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /myapp

WORKDIR /myapp

COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock

ENV BUNDLER_VERSION=2.1.4　  ← 追記です！！！

RUN gem install bundler
RUN bundle install

COPY . /myapp
```

１行だけ追記しました。

```
ENV BUNDLER_VERSION=2.1.4
```
このように、
ENVでbundlerのバージョンを環境変数で指定したところ、上手く行きました！！

## NG例（おまけ）
Dockerでは、bundlerのバージョンを指定する際、環境変数で指定しなければならないようです。
私は環境変数を設定する前に、

```
RUN gem install bundler -v 2.1.4
```
こちらの方法でbundlerのバージョンを指定しようとしましたが、上手く行きませんでした。

ご参考までに！！！
