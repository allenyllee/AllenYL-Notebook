# Git__快速上手

## 儲存認證 (只要輸入一次使用者名稱與密碼，下次不用再輸入)
* [Git - git-credential-store Documentation](https://git-scm.com/docs/git-credential-store)

    ```shell=
    $ git config credential.helper store
    $ git push http://example.com/repo.git
    Username: <type your username>
    Password: <type your password>

    [several days later]
    $ git push http://example.com/repo.git
    [your credentials are used automatically]
    ```

