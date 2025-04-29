# API2025042920250429
API練習
こんにちは！Pythonで分岐とURLの情報取得について簡単なコードをご紹介します。これは練習用のシンプルなコードです。

以下のコードはPythonでURLから情報を取得し、その内容に基づいて分岐処理を行う例です：

```python
import requests

def get_url_info(url):
    try:
        # URLからデータを取得
        response = requests.get(url)
        
        # ステータスコードによる分岐
        if response.status_code == 200:
            print(f"成功しました！ステータスコード: {response.status_code}")
            
            # コンテンツタイプによる分岐
            content_type = response.headers.get('Content-Type', '')
            if 'text/html' in content_type:
                print("HTMLコンテンツです")
                # HTMLの長さによる分岐
                if len(response.text) > 10000:
                    print("大きなHTMLファイルです")
                else:
                    print("小さなHTMLファイルです")
            elif 'application/json' in content_type:
                print("JSONコンテンツです")
                # JSONデータを解析
                try:
                    data = response.json()
                    print(f"JSONキー数: {len(data)}")
                except:
                    print("JSON解析エラー")
            else:
                print(f"その他のコンテンツタイプ: {content_type}")
                
            return response.text
        elif 400 <= response.status_code < 500:
            print(f"クライアントエラー: {response.status_code}")
            return None
        elif 500 <= response.status_code < 600:
            print(f"サーバーエラー: {response.status_code}")
            return None
        else:
            print(f"その他のステータスコード: {response.status_code}")
            return None
    except requests.exceptions.RequestException as e:
        print(f"リクエストエラー: {e}")
        return None

# 使用例
if __name__ == "__main__":
    url = "https://example.com"
    result = get_url_info(url)
    
    if result:
        print(f"取得したコンテンツの長さ: {len(result)} 文字")
    else:
        print("コンテンツを取得できませんでした")
```

このコードでは以下の分岐を行っています：
1. リクエストが成功したかどうか（ステータスコードによる分岐）
2. コンテンツタイプによる分岐（HTML、JSON、その他）
3. コンテンツの大きさによる分岐（HTMLの場合）
4. JSONの解析が成功したかどうかによる分岐

使ってみたいURLを変更して実行してみてください。例えば、異なるウェブサイトのURLや、JSONを返すAPIのエンドポイントなどを試してみると良いでしょう。
