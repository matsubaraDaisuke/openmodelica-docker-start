# openmodelica-docker-start

Docker上でOpenModelicaの開発環境を構築するためのリポジトリ

# Macの場合

XQuartzを事前にインストールして起動してください。

リポジトリのクローン

``` terminal
$ git clone https://github.com/matsubaraDaisuke/openmodelica-docker-start.git
```

ローカルのIPアドレスの取得

``` terminal
$ make IP
>> IP address: 192.168.x.xx
```

X サーバへの接続が許可されるホスト名とユーザ名をリストに追加

``` terminal
$ xhost +192.168.x.xx
```

docker-compose.ymlの環境変数(environment)を修正します

``` docker-compose.yml
services:
    openmodelica:
      container_name: openmodelica
      build: ./docker/openmodelica
      #tty: true
      environment:
        - DISPLAY=192.168.x.xx:0.0 <- HERE Edit! 
      volumes:
        - ./om-develop:/home/openmodelica
        - /tmp/.X11-unix:/tmp/.X11-unix 
```

ビルドと起動

``` terminal
$ docker-compose up --build
```

``` terminal
$ docker-compose run openmodelica /bin/bash
```

OMEditの起動

``` terminal
# OMEdit 
```

![OMEdit](https://user-images.githubusercontent.com/25544286/79966782-e778ca00-84c8-11ea-9a98-7306802c2664.png)

