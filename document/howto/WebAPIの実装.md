# WebAPIの実装
## 手順
### 追加パッケージのインストール
- Django Rest Framework
```
$ python -m pip install django-rest-framework
```
### アプリケーションの作成
`$ python manage.py startapp api`

### Djangoの設定ファイルを編集
- conndot/setting.py
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',   # 追加
    'api',              # 追加
]
```