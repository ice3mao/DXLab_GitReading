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

$ git add welcome.html

就可以把這個檔案交給 Git 來管控了。再次使用 git status 指令看一下目前的狀態：

![image](https://user-images.githubusercontent.com/43734850/155096875-ee8f799f-f002-4972-ac12-97df287c0f47.png)

剛才那個檔案從 Untracked 變成 new file 狀態了。這個表示這個檔案已經被安置到暫存區（Staging Area），等待稍後跟其它檔案一起被存到儲存庫裡。





