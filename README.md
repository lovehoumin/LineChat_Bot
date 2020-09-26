# 環境建置

### VisualStudio Code
### Python 3.6

## 註冊Heroku
### Heroku CLI https://tinyurl.com/ybqfc4wr


### git https://git-scm.com/
* mac安裝說明 https://git-scm.com/download/mac

### git安裝注意事項
![](https://github.com/lovehoumin/LineChat_Bot/blob/master/git_infor.jpg "git安裝注意事項")


# Line Chat Bot 語法說明


## 程式部屬至git

### 登入Heroku
```py
heroku login
```

### 建立git設定檔
```py
git config --global user.name
```
```py
git config --global user.email
```

### 初始化git
```py
git init
```

### 用 git 將資料夾與 heroku 連接
```py
heroku git:remote -a {HEROKU_APP_NAME}
```

### 將程式碼推上 Heroku，如果有跳出錯誤請重新輸入
```py
git add .
git commit -m "Add comment"
git push -f heroku master
```

### API使用

>回覆訊息
```py
line_bot_api.reply_message(event.reply_token, 訊息物件)
```

>主動傳送訊息
```py
line_bot_api.push_message(機器人user_ID, event.push_toker, 訊息物件)
```

### 訊息物件分類
* Text
* Sticker
* Image
* Video
* Audio
* Location
* Imagemap
* Template
* Buttons
  * MessageTemplateAction ─ 是純粹的訊息
  * URITemplateAction ─ 是網址的使用
  * PostbackTemplateAction ─ 是含有值的訊息回覆
* Confirm
  * Carousel
  * Image carousel

### TextSendMessage （文字訊息）
```py
message = TextSendMessage(text='Hello, world')
line_bot_api.reply_message(event.reply_token, message)
```

### ImageSendMessage（圖片訊息）
```py
message = ImageSendMessage(
    original_content_url='https://example.com/original.jpg',
    preview_image_url='https://example.com/preview.jpg'
)
line_bot_api.reply_message(event.reply_token, message)
```

### VideoSendMessage（影片訊息）
```py
message = VideoSendMessage(
    original_content_url='https://example.com/original.mp4',
    preview_image_url='https://example.com/preview.jpg'
)
line_bot_api.reply_message(event.reply_token, message)
```

### AudioSendMessage（音訊訊息）
```py
message = AudioSendMessage(
    original_content_url='https://example.com/original.m4a',
    duration=240000
)
line_bot_api.reply_message(event.reply_token, message)
```
### LocationSendMessage（位置訊息）
```py
message = LocationSendMessage(
    title='my location',
    address='Tokyo',
    latitude=35.65910807942215,
    longitude=139.70372892916203
)
line_bot_api.reply_message(event.reply_token, message)
```

### StickerSendMessage（貼圖訊息）
```py
message = StickerSendMessage(
    package_id='1',
    sticker_id='1'
)
line_bot_api.reply_message(event.reply_token, message)
```






























```py
from flask import Flask, request, abort

from linebot import (
    LineBotApi, WebhookHandler, 
)

from linebot.exceptions import (
    InvalidSignatureError
)

from linebot.models import *

app = Flask(__name__)

# Channel Access Token
line_bot_api = LineBotApi('qWVzBRZv0TAvrI/s7bMO+7i+olb5QDDuLs45BSRFeOatrhgDPmB4edOmtygl1j0CJY9jwFzw1/r3jTOvVNXORnWpXi4FWQMpPTm2BUcxEIdbYvIGQmI95rVjMfMvxpj39VP3t2AaDxuhE08K4JynzwdB04t89/1O/w1cDnyilFU=')
# Channel Secret
handler = WebhookHandler('d54de13f04087857389a0bb5437b7ff5')

to = 'Ufd3bc4723ce4e7f344fead08a4f171a1'

# 監聽所有來自 /callback 的 Post Request
@app.route("/callback", methods=['POST'])
def callback():
    # get X-Line-Signature header value
    signature = request.headers['X-Line-Signature']
    # get request body as text
    body = request.get_data(as_text=True)
    app.logger.info("Request body: " + body)
    # handle webhook body
    try:
        handler.handle(body, signature)
    except InvalidSignatureError:
        abort(400)
    return 'OK'

# 處理訊息
@handler.add(MessageEvent, message=TextMessage)
def handle_message(event):
    msg = event.message.text
    msg = msg.encode('utf-8')
    if event.message.text == 'Hello, World':
        line_bot_api.reply_message(event.reply_token, TextSendMessage(text=event.message.text))
    elif event.message.text == "影片":
        line_bot_api.reply_message(event.reply_token,VideoSendMessage(original_content_url='https://demo.linechatbot.cc/video.mp4', preview_image_url=r'https://img.4gamers.com.tw/ckfinder/images/Why%20Lee/event/934939bff2c5c3d4ca7e509187454bc7.png'))
    else:
        line_bot_api.reply_message(event.reply_token, TextSendMessage('Error'))
####################################分隔線####################################



def reply_message(event):
    try:
        line_bot_api.push_message(to, TextSendMessage(text='我是機器人'))
    except Exception as e:
        
        raise e


import os
if __name__ == "__main__":
    port = int(os.environ.get('PORT', 5000))
    app.run(host='0.0.0.0', port=port)

```
