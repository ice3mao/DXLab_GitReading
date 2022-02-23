### CH3 常用命令指令
![image](https://user-images.githubusercontent.com/43734850/155084532-3696a5cf-52b8-4ce4-afba-54708c37f1e8.png)
-------------------------------------------------
### CH4 設定Git

開始使用Git首先要做的第一件事（應該也只要做一次就好），就是設定使用者的 Email 信箱以及使用者名稱
開啟Terminal後輸入使用者

$ git config --global user.name "Kim Lin"

$ git config --global user.email "Kim_lin@wistron.com"

輸入完成之後，可以再檢視一下目前的設定：

$ git config --list

user.name=Kim Lin

user.email=Kim_lin@wistron.com

Git縮寫: alias Ex: checkout→co

$ git config --global alias.co checkout

$ git config --global alias.br branch

$ git config --global alias.st status

-------------------------------------------------
### CH5 開始使用Git
* 5.1 新增、初始 Repository

$ cd /tmp                  # 切換至 /tmp 目錄

$ mkdir git-practice       # 建立 git-practice 目錄

$ cd git-practice          # 切換至 git-practice 目錄

$ git init                 # 初始化這個目錄，讓 Git 對這個目錄開始進行版控

Initialized empty Git repository in /private/tmp/git-practice/.git/

![image](https://user-images.githubusercontent.com/43734850/155094835-4dcc8c5a-bcfb-4691-98f2-db9406f0519e.png)

全部就是只靠那個 .git 目錄在做事而已，所以如果這個目錄不想被版控，或是只想給客戶不含版控紀錄的內容的話，只要把那個 .git 目錄移除，Git 就對這個目錄失去控制權了。

* 5.2 把檔案交給 Git 控管

$ git status

![image](https://user-images.githubusercontent.com/43734850/155095437-c31d3570-6926-4c99-b9fc-cdd9449a83ad.png)

因為現在還沒有新增任何東西可以提交，這個目錄裡透過系統指令建立一個內容為 “hello, git” 並命名為 welcome.html 的檔案：

$ echo "hello, git" > welcome.html

![image](https://user-images.githubusercontent.com/43734850/155096075-add00e54-2615-40fe-a386-1ce9272c609a.png)

目前這個檔案是 Untracked，接下來就是要把 welcome.html 這個檔案交給 Git，讓 Git 開始「追蹤」它，使用的指令是 git add 後面加上檔案名稱：

*把檔案一道暫存區→ git add

$ git add welcome.html

就可以把這個檔案交給 Git 來管控了。再次使用 git status 指令看一下目前的狀態：

![image](https://user-images.githubusercontent.com/43734850/155096875-ee8f799f-f002-4972-ac12-97df287c0f47.png)

剛才那個檔案從 Untracked 變成 new file 狀態了。這個表示這個檔案已經被安置到暫存區（Staging Area），等待稍後跟其它檔案一起被存到儲存庫裡。

*冷知識
  * add ./ add --all 的差別
    
    git add . →  這個指令會把目前當下這個目錄及旗下子目錄，但其他外面的就不管
    
    git add --all → 指令就沒這個問題，這個專案裡所有的異動都會被加至暫存區
    
*把檔案一道儲存區→ git commit

$ git commit -m "init commit"
 
 ![image](https://user-images.githubusercontent.com/43734850/155099778-a648d752-0fff-4d57-8338-bb2eb13e69dd.png)

在後面加上的 -m "init commit" 是指要要說明「你在這次的 Commit 做了什麼事」

當完成了這個動作後，對 Git 來說就是「把暫存區的東西存放到儲存庫（Repository）裡」

* 5.3 工作區、暫存區與儲存庫

![image](https://user-images.githubusercontent.com/43734850/155100469-4d23d6b9-e729-4f39-acd4-dc0d9e9974ff.png)

1.git add 指令把檔案從工作目錄移至暫存區（或索引）。

2.git commit 指令把暫存區的內容移至儲存庫。

請記得，要執行 Commit 指令，也就是要存放到 Repository 才算是完成整個流程喔。

* 5.4 檢視紀錄

$ git log

![image](https://user-images.githubusercontent.com/43734850/155358395-48d4abf4-2e8a-4925-9d23-f4797c062dcc.png)

1. Commit 作者是誰。（人是誰殺的）

2. 什麼時候 Commit 的。（什麼時候殺的）

3. 每次的 Commit 大概做了些什麼事。（怎麼殺的）

*冷知識-5-17 SHA-1詳細介紹

那個看起來像亂碼的是一串git 根據commit的"內容"，由SHA-1生成的隨機驗證字串

SHA-1全名為security hash algorithm, 中文意思大概就是“安全加密演算法”

$ git log --oneline --graph

![image](https://user-images.githubusercontent.com/43734850/155361561-0ed2c69a-8c4f-4a7e-b9c1-da38fd968076.png)

--online還可以搭配不同條件搜尋

$ git log --oneline --author="Kim Lin"  # 找誰commit的

$ git log --oneline --since="9am" --until="12am"  # 找出「今天早上 9 點到 12 點之間所有的 Commit」

* 5.5 【狀況題】如何在 Git 裡刪除檔案或變更檔名？

# 刪除檔案 rm and git rm的差別

$ rm welcome.html 

$ git add welcome.html

如果只有rm刪除完檔案，還需要git add這次的「修改」加到暫存區

$ git rm welcome.html

而git rm狀態是 deleted，而且已被加至暫存區，所以接下來就可以進行 Commit 了

# 加上 –cached 參數

$ git rm welcome.html --cached

如果只是「我不是真的想把這個檔案刪掉，只是不想讓這個檔案再被 Git 控管了」的話，可以加上 --cached 參數

狀態從原本已經在 Git 目錄裡的 tracked 變成 Untracked

![image](https://user-images.githubusercontent.com/43734850/155366883-5cce1f36-4bb1-403a-887e-7559e019fad6.png)

# 變更檔名

$ mv hello.html world.html  # 把 hello.html 改成 world.html

但還是要git add把這次的「修改」加到暫存區

$ git mv hello.html world.html # 這樣就減少了一個步驟

* 5.6 【狀況題】修改 Commit 紀錄

# 使用 --amend 參數來修改最後一次的 Commit

![image](https://user-images.githubusercontent.com/43734850/155369637-03848477-50f5-4f1d-9ff0-1e58f6b2c16c.png)

最後一次commit的內容有點糟糕，只要直接在 Commit 指令後面加上 --amend 參數即可修改

$ git commit --amend -m "Welcome To Facebook"

![image](https://user-images.githubusercontent.com/43734850/155369969-47544732-1161-4e54-82ac-6101d61a9e3d.png)

* 5.7 【狀況題】追加檔案到最近一次的 Commit

$ git commit --amend --no-edit

--no-edit 參數的意思是指「我不要編輯 Commit 訊息」，所以就不會跳出 Vim 編輯器的視窗。
