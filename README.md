# Laravel 開発環境

## 構成

- Composer 2.7.7
- Mysql 8.0.36
- phpmyadmin
- nginx

## コマンド

### 1. プロジェクトをクローン

```shell
git clone https://github.com/makoto00000/laravel_dev_container.git
```

### 2. Laravelプロジェクトを入れるsrcディレクトリを作成

```shell
mkdir src
```

※ 必要に応じて、`php/Dockerfile`の以下の`setup_18.x`の部分をインストールしたいnodeのバージョンに書き換える。

```shell
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
```

### 3. コンテナを起動

```shell
docker-compose up -d --build
```

<details>

<summary>You don't have enough free space in /var/cache/apt/archives/.と表示される場合</summary>

Dockerの設定で、`Virtual disk limit`がデフォルトでは64GBになっていると思うので、72GBとかに増やす。

</details>

### 4. コンテナに入る

```shell
docker-compose exec php bash
```

### 5. laravelインストール

```shell
composer create-project --prefer-dist laravel/laravel ."
```

### 6. 環境ファイル修正

`.env`を編集

```shell
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=password
```

`DB_DATABASE`は適宜変更

### 7. マイグレーション

```shell
php artisan migrate
```

### 8. アクセス

- Laravel:
<http://localhost:8000>
- phpmyadmin:
<http://localhost:8080>
