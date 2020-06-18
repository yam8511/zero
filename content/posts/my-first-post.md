---
title: "Hugo + GitHub 簡易架設個人部落格"
date: 2020-06-11T03:09:06+08:00
draft: true
tags: ["first", "hugo"]
---

平時看到很多網路上的大神們都會有自己紀錄技術相關經驗的文章，忽然覺得自己也可以記錄一下自己平時遇到的技術坑or防老(?)🧐  
很早以前就知道GitHub就有提供架設靜態頁面的服務，對於純粹做前端頁面的人來說是多麼方便的功能，可以很輕易附上自己的Demo作品。  
不過從來沒有想說過可以用簡單建立純文字部落格，紀錄平時的經驗。這次剛好看到Hugo就覺得可以來好好架設簡單的部落格好好記錄一下囉!🤓  

---

# 安裝Hugo🛠

依照[官方文件🔗](https://gohugo.io/getting-started/installing/)安裝教學，其實很詳細也很簡單。  
小弟以MacOS為舉例：
```shell
> brew install hugo
> hugo version # 有正常出現版本就成功囉
Hugo Static Site Generator v0.72.0/extended darwin/amd64 BuildDate: unknown
```

---

# 開始使用🚌

1. 建立新專案

    ```shell
    > # hugo new site [專案名稱]
    > hugo new site blog
    ```

2. 先尋找自己喜歡的樣式主題

    [官方主題區🔗](https://themes.gohugo.io/)已經有提供很多漂亮又很強大的免費主題給大家套用。
    例如：我選擇[`Soho`🔗](https://themes.gohugo.io/soho/)的主題

3. 下載主題並套用
    
    3-1. 只要純粹下載主題資料夾到專案裡的`themes`資料夾內。
    ```shell
    > # 進入專案資料夾底下，下git語法
    > git clone https://github.com/alexandrevicenzi/soho.git themes/soho
    ```

    3-2. 並且在`config.toml`指定主題名稱即可完成。  
    ```toml
    # baseURL 與 title 改成自己的網址
    baseURL      = "https://yam8511.github.io/zero/" 
    languageCode = "en"
    title        = "Learn from ZerO"
    theme        = "soho" # <--- 加上剛剛下載的主題名稱
    ```

4. 新增第一份文章

    ```shell
    > # hugo new [檔案路徑/檔案名稱].md
    > hugo new posts/my-first-post.md
    ```

    上面指令就會自動幫我們建立一個新檔案在`content`資料夾底下

5. 啟動伺服器

        先啟動伺服器，預設會熱加載。
        一旦判斷檔案或config更動了，自動會重新載入。
        馬上反應到頁面上，非常方便👍

    ```shell
    > hugo server -D
                     | EN  
    -------------------+-----
    Pages            | 16  
    Paginator pages  |  0  
    Non-page files   |  0  
    Static files     |  7  
    Processed images |  0  
    Aliases          |  1  
    Sitemaps         |  1  
    Cleaned          |  0  

    Built in 48 ms
    Watching for changes in /Users/yingying/zero/zero/{archetypes,content,data,layouts,static,themes}
    Watching for config changes in /Users/yingying/zero/zero/config.toml
    Environment: "development"
    Serving pages from memory
    Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
    Web Server is available at http://localhost:1313/zero/ (bind address 127.0.0.1)
    Press Ctrl+C to stop
    ```

6. 開始瀏覽
    打開瀏覽器，輸入`baseURL`的[網址](http://localhost:1313/)，  
    以我為例就是`http://localhost:1313/zero/`

---

# 開始部署到GitHub🚀

建立美美的部落格之後，總是希望可以在網路上分享或炫砲(?)給朋友看看，所以需要有個公開的網址。  
這時候不用再煩惱伺服器的問題了，只需要使用`GitHub Pages`做部署就好囉👍  

1. 先在[GitHub](https://github.com/)建立自己的新專案

2. 在專案資料夾底下做`Git初始化`

    ```shell
    > git init
    > # git remote add origin [自己剛剛加的專案網址]
    > # 下面以小弟我的為範例
    > git remote add origin git@github.com:yam8511/zero.git
    ```

3. 打包輸出檔案 & 推上`GitHub`
    ```shell
    > # hugo -D 即是打包。 -d 表示想輸出的位子，預設是public
    > hugo -D -d ./docs # 這邊輸出到 ./docs，等等設定會用到
    > git add -A
    > git commit -m "init a blog"
    > git push origin master
    ```

4. 到設定頁面設定`GitHub Pages`

    4-1. 開啟GitHub個人專案的頁面之後，點擊`Settings`。  
    ![GitHub > Settings](/zero/github_settings.png)

    4-2. 找到`GitHub Pages` > `Source`，選擇`master branch /docs folder`
    ![GitHub Pages > Source](/zero/github_pages.png)

5. 大功告成

    等`GitHub`部署一會兒，即可在個人網址看到頁面囉。  

    網址規則是
    ```
    https://[個人帳號].github.io/[專案名稱]

    例如: https://yam8511.github.io/zero/
    ```

---

# 總結心得🤔

其實從建立到部署到完成，不用幾分鐘就可以完成。對於架設一個簡單的部落格來說，非常快速，而且又很簡單👍   
除了一般寫文章以外，其實Hugo還提供了很多可以客製化樣式或資料的設計方式，讓每個人可以寫寫文章以外，還可以客製化自己美美的部落格樣貌✨  
[官方文件🔗](https://gohugo.io/templates/introduction/)也非常齊全💯  
(有機會再寫一篇文章介紹Hugo囉😂)  

小弟自己覺得最大收益就是，用`Markdown`方式來寫文章，除了Hugo可以快速呈現頁面以外，其實對於工程師來說也方便撰寫，就算不顯示在網頁了，也能獨立打開`Markdown`檔案起來瀏覽文章。真是一箭雙鵰呀🤩  
