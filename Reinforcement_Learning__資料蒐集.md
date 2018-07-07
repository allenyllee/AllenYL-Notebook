# Reinforcement_Learning__資料蒐集


## Q Learning

- [走近流行強化學習算法：最優Q-Learning - 幫趣](http://bangqu.com/96pyt4.html#utm_source=Facebook_PicSee&utm_medium=Social)



## AlphaGO

- [Tencent/PhoenixGo: Go AI program which implement the AlphaGo Zero paper](https://github.com/Tencent/PhoenixGo)


## 魔術方塊

- [A machine has figured out Rubik’s Cube all by itself - MIT Technology Review](https://www.technologyreview.com/s/611281/a-machine-has-figured-out-rubiks-cube-all-by-itself/)

    - [[1805.07470] Solving the Rubik's Cube Without Human Knowledge](https://arxiv.org/abs/1805.07470)

        > 重點就是反向思考，從最終狀態(已解好的狀態) 慢慢轉亂，每次轉一步，產生一連串未解好的狀態，用這些未解好的狀態送進神經網路，由網路產生目前狀態的 value 跟下一步該採取行動的 policy。一開始這些值由網路隨機初始化決定，下一個狀態的reward 只有1跟-1，只有完成狀態的reward 是1，其他狀態都是-1。
        > 
        > 找出最大化reward + value的policy。這組value 跟 policy 當做訓練target，於是我們有很多訓練target，讓神經網路反覆訓練。如此，雖然只有一個reward，仍然能夠教網路學會朝向最終狀態，解決了Reinforcement Learning 中間狀態缺乏明確獎勵函數的問題。
        > 
        > [name=Ya-Lun Li] 


## 神經生物學

- [DeepMind發Nature子刊：通過元強化學習重新理解多巴胺 - 幫趣](http://bangqu.com/9T4M59.html)

## RL 論文復現

- [Lessons Learned Reproducing a Deep Reinforcement Learning Paper](http://amid.fish/reproducing-deep-rl)

## 玩遊戲

### 從結果反推

- [Learning Montezuma's Revenge from a Single Demonstration](https://blog.openai.com/learning-montezumas-revenge-from-a-single-demonstration/)

    ![](https://blog.openai.com/content/images/2018/06/montezuma_graphic@2x.png)

