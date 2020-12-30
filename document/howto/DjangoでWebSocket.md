# DjangoでWebSocket
## 参考資料
- [Django Channels](https://channels.readthedocs.io/en/stable/)
- [Django ChannelsでできるリアルタイムWeb](https://qiita.com/massa142/items/cbd508efe0c45b618b34)

## 手順
### 


## [Tutorial](https://channels.readthedocs.io/en/stable/tutorial/part_1.html)
### [Tutorial Part 1: Basic Setup](https://channels.readthedocs.io/en/stable/tutorial/part_1.html)
1. `pip install -U channels`
2. `python manage.py startapp chat`
3. 不要ファイルの削除
4. INSTALLED_APPにchatを追加
5. テンプレートの追加
6. ルーティングの追加(urls.py, views.py)
7. 疎通確認
8. ASGIの設定と疎通確認
  - [ASGI(Asynchronous Server Gateway Interface)に関する説明](https://cocolofun.com/django-channels/)

### [Tutorial Part 2: Implement a Chat Server](https://channels.readthedocs.io/en/stable/tutorial/part_2.html)
1. テンプレートの追加(room)
2. スクリプトの記述(room)
3. ルーティングの追加(room)
4. 疎通確認(リダイレクトされるところまで)
```
(index):15 WebSocket connection to 'ws://127.0.0.1:8000/ws/chatnull/' failed: Error during WebSocket handshake: Unexpected response code: 500
```
5. consumerの追加
```
It is good practice to use a common path prefix like /ws/ to distinguish WebSocket connections from ordinary HTTP connections because it will make deploying Channels to a production environment in certain configurations easier.

In particular for large sites it will be possible to configure a production-grade HTTP server like nginx to route requests based on path to either (1) a production-grade WSGI server like Gunicorn+Django for ordinary HTTP requests or (2) a production-grade ASGI server like Daphne+Channels for WebSocket requests.

Note that for smaller sites you can use a simpler deployment strategy where Daphne serves all requests - HTTP and WebSocket - rather than having a separate WSGI server. In this deployment configuration no common path prefix like /ws/ is necessary.
```
6. consumerに対するルーティングの追加
7. ASGIにwebsocket通信を定義
8. マイグレーションを実行
  - この時点で単一consumerでのWebsocket通信が疎通可能
  - 複数consumer間でのやりとりを行うため、次項でchannelを有効化する
9. チャンネルレイヤーの有効化
  - Redisサーバーを使う
  - dockerのredisコンテナを起動する  
  `$ docker run -p 6379 -d redis:5`
  - `$ python -m pip install channels_redis`
  - {mysite}/setting.pyにCHANNEL_LAYERSの設定を追加
  ```
  It is possible to have multiple channel layers configured. However most projects will just use a single 'default' channel layer.
  ```
  - [Django shell](https://hodalog.com/how-to-use-django-shell/)からredisとの疎通を確認
    - やってることは`test_channel'というキーにJSON文字列を紐づけてredisへ保存⇒アクセスしてるだけ
  - こんなのがでた  
  `ConnectionRefusedError: [Errno 10061] Connect call failed`
    - [Windowsだと問題が出る場合がある模様?](https://stackoverflow.com/questions/64227425/connectionrefusederror-errno-10061-connect-call-failed-127-0-0-1-6379-we)
    ```
    If you are using Windows, some troubles may arise. django-channels comes packaged with redis and in-memory channel layers. Generally, in development you don't have to use redis, just redefine channel layers backend option:
    ------------------------------------------------------------
    # setting.py
    CHANNEL_LAYERS = {
        "default": {
            "BACKEND": "channels.layers.InMemoryChannelLayer"
        }
    }
    ```
    - そんなことはなく、Redisコンテナのホスト側ポートを指定し忘れていただけ
  - chatConsumerからredisを参照してチャンネル管理できるように改修
- ※WinMergeの差分確認でalias指定してなかったので設定した
```
[alias]
    windiff = difftool -y -d -t WinMerge
```


