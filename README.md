# 環境建置

### VisualStudio Code
### Python 3.6

## 註冊Heroku
### Heroku CLI https://tinyurl.com/ybqfc4wr


### Git https://git-scm.com/
* mac安裝說明 https://git-scm.com/download/mac




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

