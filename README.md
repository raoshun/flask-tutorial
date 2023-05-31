# flask-tutorial

pythonのWebフレームワークであるFlaskを試してみる。  
参考ページ
- [DockerでFlaskを実行するコンテナを作る](https://gray-code.com/blog/flask-on-docker/)
- [Flaskへようこそ — Flask Documentation (2.2.x)](https://msiz07-flask-docs-ja.readthedocs.io/ja/latest/index.html)

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

## ページを作る

### テンプレートを作る
ページを作る際には、ページ構成を定義したテンプレートを作る。例として`app/templates/index.html`を挙げる。
```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>Flask</title>
</head>
<body>
  <h1>Welcome to Flask!</h1>
  <p>Hello, {{ data.name }}</p>
</body>
</html>
```
中身は基本的に通常のhtml形式で記述する。通常と異なるのは、`{{}}`で囲まれた部分で、内部処理の呼び出し元で指定された値に置き換えられる。

### テンプレートを呼び出す
作ったテンプレートをURLと紐づける。先ほどのテンプレートをトップページのテンプレートとして読み込んでみる。`index.py`にある以下の記述がトップページを表示するためのコードにあたる。
```python
# Top Page
@app.route("/")
def index():
    values = {"name": "Taro"}
    return render_template('index.html', data=values)
```

ポイントは2点。
1. デコレータ`@app.route("/")`を関数につけて、ページのパスを定義する
2. 関数の戻り値に`flask.render_template`を与え、関数の引数に前述のテンプレートと、テンプレート内部で使用している変数を定義した辞書を渡す

# todo

* CSSで装飾する
* 開発のベストプラクティス（VSCodeの開発コンテナなど）
* Plotlyとの融合