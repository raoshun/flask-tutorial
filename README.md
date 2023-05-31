# flask-tutorial

pythonのWebフレームワークであるFlaskを試してみる。
<cite>[DockerでFlaskを実行するコンテナを作る](https://gray-code.com/blog/flask-on-docker/)</cite>

# hello worldの実行

docker imageをbuildする。
```sh
$ docker image build -t flask .
```

完成したimageからコンテナを起動する。
```sh
$ docker run --rm -p 5000:80 -v ${PWD}/app:/app flask
```

無事に実行できていればlocalhost:5000にアクセスするとHello, Flask!と書かれたページが表示される。  
コンテナを止めるときはCtrl＋C。