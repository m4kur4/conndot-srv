# DjangoでWebSocket
## 参考資料
- [Django Channels](https://channels.readthedocs.io/en/stable/)
- [Django ChannelsでできるリアルタイムWeb](https://qiita.com/massa142/items/cbd508efe0c45b618b34)

## 手順
### 


## チュートリアル「chat」
### セットアップ
[Tutorial](https://channels.readthedocs.io/en/stable/tutorial/part_1.html)
1. `pip install -U channels`
2. `python manage.py startapp chat`
3. 不要ファイルの削除
4. INSTALLED_APPにchatを追加
5. テンプレートの追加
6. urls.pyの設定(アプリ側)
7. urls.pyの設定(本体側,chatをインクルード)
8. 疎通確認
9. ASGIの設定と疎通確認
  - [ASGI(Asynchronous Server Gateway Interface)に関する説明](https://cocolofun.com/django-channels/)
### 