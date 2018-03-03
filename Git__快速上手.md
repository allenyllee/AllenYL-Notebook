# Git__快速上手

<!-- toc --> 
[toc]


- 第一次 commit 時，需要設定 user.email 和 user.name，此處只是用來記錄是哪一個 user 做 commit，方便辨認，不一定要跟登入帳號相同

    ```shell
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    ```
    ![](https://screenshotscdn.firefoxusercontent.com/images/2579ef82-bf21-4c84-b9fd-f078e755acb0.png)




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

