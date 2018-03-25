# DevOps__開發維運

## Continueous Integration

- [Turbo Charge Agile Processes with Deep Learning – Intuition Machine – Medium](https://medium.com/intuitionmachine/deep-learning-enables-agile-processes-6cfc353fa9b2)

- [Continuous Integration on your Machine/Deep Learning models with Moven – SSIX](https://ssix-project.eu/continuous-integration-with-moven/)

- [Moven, Machine/Deep Learning models distribution relying on the Maven infrastructure – SSIX](https://ssix-project.eu/moven-machinedeep-learning-models-distribution-relying-on-the-maven-infrastructure/)

- [Test-Driven Development for Data Science · Pivotal Engineering Journal](http://engineering.pivotal.io/post/test-driven-development-for-data-science/)

- [Continuous Integration for Data Science · Pivotal Engineering Journal](http://engineering.pivotal.io/post/continuous-integration-for-data-science/)

- [Continuous delivery for machine learning](https://www.slideshare.net/RajeshMuppalla/continuous-delivery-for-machine-learning-82257558)


## CI with Jenkins

Jenkins 的設定截圖，參考一下

1.  到管理Jenkins>系統設定>新增雲>Yet Another Docker
2.  在 Yet Another Docker 面板輸入Docker 所在URL ([localhost:4243](http://localhost:4243)) (這部份需要設定啟動 Docker API) 參考以下script  
    
    ```shell
    ######################
    # enable docker api for jenkins CI use
    # Enabling Docker Remote API on Ubuntu 16.04 – The Blog of Ivan Krizsan
    # [https://www.ivankrizsan.se/2016/05/18/enabling-docker-remote-api-on-ubuntu-16-04/](https://www.ivankrizsan.se/2016/05/18/enabling-docker-remote-api-on-ubuntu-16-04/)
    # test: curl [http://localhost:4243/version](http://localhost:4243/version)
    # test2: curl -X GET [http://192.168.5.5:4243/images/json](http://192.168.5.5:4243/images/json)
    ######################
    sudo sed -i '/ExecStart=\\/usr\\/bin\\/docker*/ c\\ExecStart=\\/usr\\/bin\\/dockerd\\/ -H fd:\\/\\/ -H tcp:\\/\\/[0.0.0.0:4243](http://0.0.0.0:4243)\\/' /lib/systemd/system/docker.service
    systemctl daemon-reload
    sudo service docker restart
    ```
      
    
3.  Image name 填上 `evarga/jenkins-slave` (目前只有測過這個image是可用的，但這個image裡面是ubuntu，所以要參考一下他的dockerfile，改寫成其他OS對應的套件，再build一個新的image出來)
    
    [evarga/jenkins-slave - Docker Hub](https://hub.docker.com/r/evarga/jenkins-slave/~/dockerfile/)
    
4.  label 可隨便填，之後會用到(這裡填another-docker) 
    
5.  launch method 選 Docker SSH computer launcher，credential 填登入image的帳號密碼(那個image的設定是 jenkins:jenkins) 

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.2&disp=emb&attbid=ANGjdJ9rsKN_9N3hW7g5MN-9np8GukKBUyKJ9dT5QUi4wK94C8ezHy6MsWy6EkFhQCUn0w9Ds8_BO0BuJxjz6eEgP6bGnG2UGdjKCQqYa67uoDynmQUjN8WtkobHayc&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  
  

6. 主畫面選擇 新增作業  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.3&disp=emb&attbid=ANGjdJ9OgjFcZoMxsbZmCX2uEdC7nTf5YdK6RN3EtJV8j-tvfsH5xjsysDGjgPeyVPRdJK7Sp5JkwIXonxrRIxhMKI4_Ekxsw_fJiJ1GzdPjVNh8YGaMVuvcQobZ5K0&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  

  

7. 輸入專案名稱，選擇建置Free-Style 軟體專案，按ok  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.4&disp=emb&attbid=ANGjdJ_HbTb4MbBTIVeig6Of7x5NpxvzCfLulRMYSrv4TBn0UHGZq9YGqi1RyEgFE4D3lShM3mAraDA1QuhcYM_hqPqxc5ttmzZkSKDVXO7VHA-qB5jWPJTzcaPzoHo&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  
  

8. 限制執行節點 填入 another-docker，在執行shell 中填入`echo hello world`


    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.1&disp=emb&attbid=ANGjdJ8rlMHD6OIDDXVZlomz_BCWoF57ldGGkkybqpwKfiuouDzkcUogGaO9yui12GX9-bZK-4FD8dhxTsLXwgVYDbyu-9gzlsYLJ01WVyIBsDKuOpd6UYrq-FQqr2Q&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  

  

  

9. 按下 馬上建置，過一陣子建置歷程中會出現一條紀錄，點進去可以看見內容  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.5&disp=emb&attbid=ANGjdJ_3ReJfVYImessuDwtaJU9BJLtzkkxpu8r_F70Mb_HP5x5xcoByvUWWk_h5wxmYOZuaxItp7il4xvyYXUWuXKgku_x4Up75zCEnMnBWQYjF8JS_yi9gmQQYQyc&sz=s0-l75-ft&ats=1521905790350&rm=15f2df6dd368d970&zw&atsh=1)  

  

  

10. 點入Console Output 可以看見 執行結果，這個結果表示在該docker image 中執行echo hello world 成功

    這表示可以執行任何command，可以執行git clone XXX 把 code 抓下來，也可以透過 gitlab-plugin 作到這件事

    [jenkinsci/gitlab-plugin: A Jenkins plugin for interfacing with GitLab](https://github.com/jenkinsci/gitlab-plugin)

    如果失敗的話就會return error code，這裡的狀態就會顯示錯誤  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.6&disp=emb&attbid=ANGjdJ-3Ig78Cn2zrrscPkOjRpr1ty3mXK-4Wc0p01u1pjCmORKmu-NDSUedyV3yacCyU1SkhljUwBwMjRBl_KXJ3wqPO8LM_GkMoEgPwHRFf9pg7H9s5ZLhFrLM9no&sz=s0-l75-ft&ats=1521905790350&rm=15f2df6dd368d970&zw&atsh=1)  
  

  

11. 如果需要build 完可以直接燒到機台上的話，可能要修改docker run 的設定，加上 `--privileged` 參數 應該就可以access NVMe device

    這樣就可以執行燒錄，或其他的測試 script，中間如果發生任何意外中斷的話，就會直接 return failed

    (可以在所有的測試機台上安裝docker client，在 Yet Another Docker 的地方選擇 Add Docker Template，輸入測試機台的url，就可在所有機台上進行自動測試，但windows 可能還沒辦法，主要原因是windows 的docker client 是跑在虛擬機中，沒有辦法access real HW，也許未來會支援吧，可以關注一下) 

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.7&disp=emb&attbid=ANGjdJ-sefQKTrCCwrBcx66uumuhJfghe8Rx_dF8wnjj13WlEuTlZWfYNiMGeA7Ey4yYzWHcIN7lQyBnSqUTrhZajluscddnKDdXIWKSnvj-Uw5jmMuzEt79ULlo1vo&sz=s0-l75-ft&ats=1521905790350&rm=15f2df6dd368d970&zw&atsh=1)




## CI for Machine Learning Project

- [Continuous Integration for ML Projects – Onfido Tech – Medium](https://medium.com/onfido-tech/continuous-integration-for-ml-projects-e11bc1a4d34f)

    > Jenkins is our continuous integration system of choice and we use it for building and deploying applications. All of our repos contain a Jenkinsfile which defines the pipeline that Jenkins will execute. Most common steps of the pipeline are:
    > 
    > -   Build a Docker image
    > -   Run our unit/integration test (within a instance of that Docker image)
    > -   Run acceptance tests (end-to-end, may require some orchestration)
    > -   Deploy to staging and production
    > 
    > Every time developer pushes their code to remote git server, Jenkins reads the pipeline file and follows the appropriate steps. Having this pipeline define for each repository has proven to give us a lot of flexibility to each service steps.
    > 
    > Here is a visualization of these processes:

    > ![](https://cdn-images-1.medium.com/max/1200/1*b1N4Scplrl0SPIkPfIU4wA.png)


    > #### **Testing models before deploying**
    > 
    > As we do with all other software, before we release changes to ML models we want to have a certain degree of confidence that our changes have not negatively impacted how our system behaves (at least in unexpected ways). But how can we be confident that our models perform as we expect them?
    > 
    > The solution we found is to introduce a new type of test in our test suite: **accuracy tests**.
    > 
    > An accuracy test exercises the inference code for a test data sample for a model to verify that the output is above an expected threshold.
    > 
    > If you remember our CI lifecycle above, we made the following changes:
    > 
    > -   Allow docker image building step to resolve the model dependencies
    > -   Run unit/integration tests (fast to fail)
    > -   Run acceptance test (usually slower than the previous set)
    > -   Download the test dataset (currently using S3 to store this information)
    > -   Trigger the accuracy tests (speed can vary greatly depending on hardware, sample size, etc.)
    > 
    > With this setup, we have a high degree of confidence when making changes in our services that the performance of models have been unaffected — enabling us to move a lot faster.
    > 
    > As this runs inside a container, we can also run these tests locally.
    > 
    > In some scenarios, we have had to make different compromises:
    > 
    > -   For services using small and fast inference models, we can use small (but still statistically significant) test datasets which — with some parallelising — can run on every build and finish in seconds/minutes
    > -   For other services using models with higher resource needs/slower inference time, we chose to run them on a scheduled basis on integration branches. This balances time for feedback with certainty that we’ll still catch regressions before they reach production
    > 
    > At this point we have a system that allows us to add new models, make change with confidence and deploy to production in a streamlined way. The pipeline looks similar to before:
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*N6L8T495ii4EZFEzgZZbow.png)
    > 
    > Pipeline after the introduction of ML models


- [Don’t be afraid of the big bad blob! – Onfido Tech – Medium](https://medium.com/onfido-tech/dont-be-afraid-of-the-big-bad-blob-3da567f7a67b)

    > If you’re familiar with machine learning, you probably know that these trained models can sometimes get pretty big, up to multiple GBs per model.
    > 
    > Now, think of these models stored in your Git repository. Every change in these large files causes the repository to grow by the size of the file. You can then easily get a repository that weights dozens of GBs, which is much harder to maintain — and not really what Git was built for.

    > After spending quite some time in researching and brainstorming, we came up with the following architecture
    >
    > ![](https://cdn-images-1.medium.com/max/1200/1*dnUxUa1uBUoy7TgJU1eWIA.jpeg)
    >
    > We have our code repository. Part of that repository is the Dockerfile which includes a specific instruction to resolve all the dependencies of the project as described in the dependencies.json file.
    > 
    > Each dependency is provided with its path of where it can be found, and the version required for it.
    > 
    > All of the dependencies are stored in S3 which is a fast, reliable, scalable and robust remote file storage.
    > 
    > #### Architecture in depth
    > 
    > Our models are being stored and versioned in an S3 bucket by our machine learning engineers. This architecture scales easily to help us industrialise our machine learning pipelines.
    > 
    > This led us to develop and recently open-source the [s3-uploader](https://github.com/onfido/s3-uploader) command line tool. This command line tool is written in Python, and its purpose is to upload any resource to S3 while taking care of the versioning for you.
    > 
    > To use it, one just simply needs to run the following command:
    > ```shell
    > s3-uploader -b s3-bucket -f /path/to/large_blob -l project/blobs/data/
    > ```
    > Where you only need to provide the **name of your bucket**, the **path to the blob** and **the location in which the blob should be placed in your project**. After that, you’ll get the json output to add to the dependencies.json file.
    > 
    > Inside the code repository, we have the dependencies.json file which is a configuration file that provides all of the project’s dependencies that are not stored in git. The file content is as follows:
    > 
    > ```json
    > { 
    >   "dependencies": [ 
    >     { 
    >       "location": "project/models/data/", 
    >       "name": "trained_model", 
    >       "version": "2017-03-27-15-22-20" 
    >     }, 
    >     { 
    >       "location": "project/blobs/data/", 
    >       "name": "large_blob", 
    >       "version": "latest" 
    >     } 
    >   ], 
    >   "repository": "s3://s3-bucket" 
    > }
    > ```
    > 
    > In addition, we have the Dockerfile which contains all the instructions to build a docker container with all the code and the trained models that later will be deployed and run on Kubernetes.
    > 
    > The part of the Dockerfile that is in charge of resolving all the project’s dependencies is this one-liner:
    > ```dockerfile
    > # Resolve project's dependencies
    > 
    > RUN dependencies-resolver -c dependencies.json
    > ```
    > 
    > This led us to develop and recently open-source the [dependencies-resolver](https://github.com/onfido/dependencies-resolver) command line tool. The command line tool is written in Python and handles all the project’s S3 dependencies for you. In our use-case, the resolver use defined in the Dockerfile. While building the container, the resolver downloads all the dependencies and places them in their specified location. The tool is not required to run as part of the Dockerfile and can be used outside of that context.
    > 


## 文字 DevOpts (Literate DevOps)

- [Literate DevOps](http://howardism.org/Technical/Emacs/literate-devops.html)

    > Maintaining servers falls into two phases:
    > 
    > 1.  Bang head until server works
    > 2.  Capture effort into some automation tool like Puppet or Chef.
    > 
    > Recently, I’ve been playing around with making the first phase closer to the second. For lack of a better word, I’m calling it _literate devops_.

### 使用 Jupyter Notebook 實現文字 DevOpts (Literate DevOps)

- 範例:
    - [literate-ops/10k-single-jupyterhub.ipynb at master · allenyllee/literate-ops](https://github.com/allenyllee/literate-ops/blob/master/10k-single-jupyterhub.ipynb)

