LNMP 开发环境
=============

基于 `Docker` 容器的 `PHP` 本地开发环境.

本地只安装 `Nginx` 和 `PHP`, `MaraiDB` 和 `Redis` 直接在应用配置连接 `dev` 环境的.

### 使用
第一次运行，需要 `--build` 参数，构建镜像并运行容器
```bash
$ docker-compose up --build -d
```

之后，直接启动容器即可
```bash
$ docker-compose up -d
```

### 说明
#### 版本
若需要指定 `PHP` 的某个版本，修改 `docker-compose.yml`.
```
args:
  - PHP_VERSION=7.1.18 # 指定 PHP 版本
```
> 修改之后需要重新构建镜像

#### 应用
应用直接放在 `www` 目录即可，例如：`www/demo`  
然后在 `nginx/conf.d` 目录配置应用 `demo.conf` 即可.

若 `nginx` 容器已运行，则要重新加载配置，`PHP` 同理.
```
$ docker exec nginx nginx -s reload
```
