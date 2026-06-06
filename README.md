# アパレルECサイト　2026年度版

## 概要
アパレル商品を販売するECサイトです。
ユーザーは商品を閲覧・購入ができます。また、管理者側では商品を管理する事ができます。
実装を想定して、要件定義から設計・開発まで一貫して行なっています。

## 使用技術
- PHP
- Laravel
- Blade
- TailwindCSS
- Vite
- Docker
- MySQl
- Git/Github

## 主な機能
ユーザー登録機能
商品一覧表示
商品詳細表示
カート機能
商品購入機能
管理者による商品管理機能

## ブランチ戦略
- main
本番用ブランチ
- feature/機能名
機能開発用ブランチ
- fix/機能名
修正用ブランチ
機能ごとにmainブランチから切って開発。開発終了後mainブランチにマージ

##　開発手法
ウォーターフォール開発

## 環境環境
Dcoker Composeを利用して構築予定

## コンテナ構成
- app（Laravel）
- nginx
- mysql
- redis
- mailpit

## セットアップ
1. リポジトリ取得
git clone https://github.com/kei3781/apparel-ec-portfolio.git
cd apparel-ec-portfolio
2. Docker起動
docker compose up -d
3. Laravelセットアップ
docker compose exec app composer install
docker compose exec app php artisan key:generate
docker compose exec app php artisan migrate
4. アクセス
http://localhost:8000

＊開発の進行に合わせて追記
2026.6/6版