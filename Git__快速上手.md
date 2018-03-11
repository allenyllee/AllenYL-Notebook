# Git__快速上手

<!-- toc --> 
[toc]



## 如何將別人的 git 倉庫複製回來再推送到自己的 gitlab

- 到別人的 git 倉庫 (git repositry) 把位址複製下來，記得選HTTPS
    ![](https://screenshotscdn.firefoxusercontent.com/images/47e74335-71f0-41a3-817d-fcba2fc05ac5.png)

- 到 termimnal 中輸入:
    
    ```git clone https://foo/bar.git mybar```
    
    其中位址 `https://foo/bar.git` 改成上一步得到的倉庫位址，`mybar` 改成你要存放的資料夾名稱(預設會用倉庫位址 `xxx.git` 中的 `xxx` 為資料夾名稱)
    
    ![](https://screenshotscdn.firefoxusercontent.com/images/e743e848-bcbf-4902-b2a1-82c9e81aeba8.png)

- 輸入 `ls -l` 會發現新增的資料夾，`cd` 到該資料夾
    
    ![](https://screenshotscdn.firefoxusercontent.com/images/180e74ee-0b58-49d8-a84f-7fc4390bb12d.png)

- 到你自己的 gitlab 網頁新增一個 project
![](https://screenshotscdn.firefoxusercontent.com/images/4020ac49-4d35-4147-8cca-b0c3805032bd.png)

- 輸入 project 名稱，若不想公開，選擇 private
![](https://screenshotscdn.firefoxusercontent.com/images/5b320a33-0a09-4516-8dfd-17ad2564d588.png)

- 複製 project 位址，假設是 `https://myname/bar.git`
![](https://screenshotscdn.firefoxusercontent.com/images/054264d7-ae1c-47a5-a07e-6e175d4a3331.png)

- 回到 terminal，輸入:

    `git remote add myremote https://myname/bar.git`
    
    上面會將你的位址命名為`myremote`，加入遠端列表，可改成自己想要的名字，再輸入：
    
    `git push myremote`
    
    即可將資料傳到你自己的gitlab上
    
    ![](https://screenshotscdn.firefoxusercontent.com/images/6b668c8f-a614-49ad-9e42-78b37463bc30.png)

## 如何將修改過的檔案推送到自己的 gitlab

- 假設你修改了一些檔案，又新增了一些檔案，然後輸入 `git status`，就會發現用紅字顯示修改過的檔案及新增的未追蹤檔案
    
    ![](https://screenshotscdn.firefoxusercontent.com/images/8c016b6e-64a3-48c4-9f3b-c14fad59236e.png)

- 假設你想要將某檔案或某路徑排除，有可能是一些自動產生的暫存檔案之類的，輸入 `echo "path/want/to/exclude" >> .gitignore` 將路徑加到 `.gitignore` 排除清單，之後再輸入一次 `git status` ，此時排除的檔案就會消失，並新增一個 `.gitignore` 檔案

    ![](https://screenshotscdn.firefoxusercontent.com/images/2789d578-2402-487d-b502-66707aa1f772.png)

- 輸入`git add .` 就會將所有修改新增的檔案加入暫存，以綠色字表示

    ![](https://screenshotscdn.firefoxusercontent.com/images/79106444-b54d-40e2-b90b-fafb81dd46f5.png)

    - 如果只想加入某個檔案，假設檔名是 _foo.bar_ ，可以輸入 `git add foo.bar`
    - 如果想一次加入相同副檔名的檔案，可以輸入`git add *.bar`

    - 這一步若不小心加錯檔案了，可以下 `git reset HEAD` 回復成紅字狀態

- 輸入 `git commit -m "some messages..."` 將剛剛加入暫存的檔案提交出去，並附上一段訊息，輸入 `git log` 可以查看提交訊息
    
    ![](https://screenshotscdn.firefoxusercontent.com/images/e2250aad-de6b-4976-8ad5-de90b77664c7.png)
    - 第一次 commit 時，需要設定 user.email 和 user.name，此處只是用來記錄是哪一個 user 做 commit，方便辨認，不一定要跟登入帳號相同

        ```shell
        git config --global user.email "you@example.com"
        git config --global user.name "Your Name"
        ```
        ![](https://screenshotscdn.firefoxusercontent.com/images/2579ef82-bf21-4c84-b9fd-f078e755acb0.png)

    - 這一步如果不小心做錯了，可以下 `git reset HEAD^` ( 注意多了一個帽子hat`^` )，就會回到上一步紅字狀態
    - 如果想退回前兩版，就下 `git reset HEAD^^` (加兩個帽子 `^^`)
    - 如果想退回前三版，下 `git reset HEAD~3` (接數字3)，前N版就接數字N，依此類推

- 輸入 `git push myremote` 即可將資料傳到你自己的 gitlab 上

    ![](https://screenshotscdn.firefoxusercontent.com/images/4a33e784-aa39-42a1-85b2-b60cba103f56.png)

    - 這一步如果做錯，因為已經上傳到server了，就必須要強制複寫server 的紀錄，可以下 `git push myremote --force` 將修正過的版本複寫上去。(注意:複寫後就無法再回復了，慎用！)

## 如何拉取遠端的更新

- 先從所有的遠端抓取更新 `git fetch --all`
    - 如果只想抓某個遠端的更新，可下 `git fetch myremote` myremote 換成你指定的遠端名，預設的遠端名稱是 origin，就是你複製的源頭

- 輸入 `git pull origin master` 就會從最開始複製的遠端位址的 master 分支抓取更新；同理，輸入 `git pull myremote master` 就會從自己的 gitlab 的 master 分支抓取更新

    ![](https://screenshotscdn.firefoxusercontent.com/images/62e93de3-6188-47b3-8cfe-06ca742f846a.png)

## 拆分工作建立分支 branch，避免與主分支打架

## 將其他分支的工作 merge 到自己的分支


## 從版本控管中隱藏/移除

- 有些檔案你想保留一份原始版本讓大家可以下載，但某些原因他每次都會更新 (例如：build code 時自動更新日期...等) 導致一直出現在變更檔案列表中，你想要暫時忽略這種變更，使用 `git update-index --assume-unchanged path/to/file`

    - [github - Untrack files from git temporarily - Stack Overflow](https://stackoverflow.com/questions/6964297/untrack-files-from-git-temporarily)

        > [git update-index](http://www.kernel.org/pub/software/scm/git/docs/git-update-index.html) should do what you want
        > 
        > This will tell git you want to start ignoring the changes to the file  
        > `git update-index --assume-unchanged path/to/file`
        > 
        > When you want to start keeping track again  
        > `git update-index --no-assume-unchanged path/to/file`

- 有些檔案你想將之從版本控管中移除，讓其他人也看不到，使用 `git rm --cached`

    > @Ehsan it seems `git rm --cached` will lead to a deletion of the local copies on other machines, where the same branch is checked out, on their next pull. See [arlocarreon.com/blog/git/…](http://www.arlocarreon.com/blog/git/untrack-files-in-git-repos-without-deleting-them/) and especially the discussion below it. – [mit](https://stackoverflow.com/users/362951/mit "5,851 reputation") [Aug 30 '15 at 11:12](https://stackoverflow.com/questions/6964297/untrack-files-from-git-temporarily#comment52468634_6964322)


## git lfs 上傳二進位大檔案

- 有時候你需要上傳二進位大檔案，例如圖片、影像、執行檔等等，就需要使用到git lfs 來管理大檔案。
    
    git lfs 需要在本地端與server 同時支援，如果你已經裝好了，server 也支援(gitlab預設支援) ， 下`git lfs track '*.bar'` 把 `*.bar` 換成你的檔案名，然後會產生一個 _.gitattributes_ 檔，接下來的操作就一樣，`git add xxx`，記得把 _.gitattributes_ 也加進去。

    - [Tutorial · git-lfs/git-lfs Wiki](https://github.com/git-lfs/git-lfs/wiki/Tutorial)

        To see a list of all patterns currently being track by git-lfs, run `git lfs track` with no arguments

        ```
        Listing tracked paths
            *.bin (.gitattributes)
        ```
        To see the list of files being track by git-lfs, run `git lfs ls-files`.




## 儲存認證 (只要輸入一次使用者名稱與密碼，下次不用再輸入)

* [Git - git-credential-store Documentation](https://git-scm.com/docs/git-credential-store)

    > ```shell
    > $ git config credential.helper store
    > $ git push http://example.com/repo.git
    > Username: <type your username>
    > Password: <type your password>
    > 
    > [several days later]
    > $ git push http://example.com/repo.git
    > [your credentials are used automatically]
    > ```


## 取得根目錄

- [version control - Is there a way to get the git root directory in one command? - Stack Overflow](https://stackoverflow.com/questions/957928/is-there-a-way-to-get-the-git-root-directory-in-one-command)
    > Yes:
    > 
    > ```shell
    > git rev-parse --show-toplevel
    > ```


## 加入忽略清單

- [gitignore - Is there an ignore command for git like there is for svn? - Stack Overflow](https://stackoverflow.com/questions/1677121/is-there-an-ignore-command-for-git-like-there-is-for-svn/19659214)
    
    > On Linux/Unix You can append files to the .gitignore file with the `echo` command. For example if you want to ignore all `.svn` folders, run this from the root of the project:
    > 
    > ```shell
    > echo .svn/ >> .gitignore
    > ```

## Troubleshooting

- [How to download files when git-lfs was installed after git clone · Issue #325 · git-lfs/git-lfs](https://github.com/git-lfs/git-lfs/issues/325)

    > -   git-lfs is not installed
    > -   clone a repository containing large files (i.e. using git-lfs)
    > -   large files are actually text pointers (OK)
    > -   install git-lfs
    > 
    > -\> large files are still text pointers
    > 
    > How can I "refresh" my local repository so that git-lfs replaces the text pointers with the actual files?

    > Update for those interested: since v0.5.2 `git lfs fetch` does the job!

    > Another update: `git lfs pull` is now the correct command, as of Git LFS v0.6.0. `fetch` will download the files, but `pull` updates them in the working directory.

    如果已經確定安裝 git-lfs，先 checkout 到另外一個 branch，再切回來 ，這樣應該會自動下載


