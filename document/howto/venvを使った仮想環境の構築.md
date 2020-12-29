# venvを使った仮想環境の構築
## 参考資料
- [仮想環境とパッケージ](https://docs.python.org/ja/3/tutorial/venv.html)

## 環境
```bash
$ python --version
Python 3.8.5
```

## 手順
### pipのアップグレード
- `--user`オプションを付けないとWindowsは権限で弾かれる(sudoないので)
`$ python -m pip install --upgrade pip --user`

### venvのインストール
`pip install virtualenv --user`
```bash
$ virtualenv --version
16.7.2
```

### 仮想環境を新規に作成
`python -m venv {env-name}`

### 仮想環境の有効化
```bash
$ source ./{env-name}/Scripts/activate
```

### (パッケージインストール後)requirements.txtの出力
`$ pip freeze > requirements.txt`

### パッケージの移植
`$ pip install -r requirements.txt`