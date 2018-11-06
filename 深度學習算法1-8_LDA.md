# 深度學習算法1-8_LDA

## LDA

$$
\begin{split}
&遊戲中的K個topic-word骰子，可記為\vec{\varphi_{1}},...,\vec{\varphi_{K}}，\\
&對於包含M篇文檔的語料庫C=(d_1,d_2,...,d_M)\\
&中的每篇文檔d_m，都有一個特定的doc-topic骰子\vec{\theta_{m}}，\\
&所有對應的骰子記為\vec{\theta_{1}},...,\vec{\theta_{M}}\\
&\\
&由條件機率，第m篇文檔d_m中的每個詞的生成機率可展開為\\
&p(w|d_m)=\displaystyle\sum_{z=1}^{K}p(w|z)p(z|d_m)=\sum_{z=1}^{K}\varphi_{zw}\theta_{mz}\\
&所以整篇文檔的生成機率為\\
&p(\vec{w}|d_m)=\displaystyle\prod_{i=1}^{n}\sum_{z=1}^{K}p(w_i|z)p(z|d_m)=\prod_{i=1}^{n}\sum_{z=1}^{K}\varphi_{zw_i}\theta_{dz}
\end{split}
$$

---

$$
\begin{split}
&\vec{\theta_m} \sim Dir(\vec{\alpha})\\
&\vec{\varphi_k} \sim Dir(\vec{\beta})
\end{split}
$$

---

$$
\begin{split}
&\vec{\alpha} \rightarrow \vec{\theta_m} \rightarrow z_{m,n} : 這個過程表示如何生成第m篇文檔\\
&第n個詞的topic編號。從第一個罈子抽出M個骰子，\\
&其中的第m個骰子作為這篇文檔的doc-topic骰子\vec{\theta_m}，\\
&然後投擲這個骰子生成文檔中第n個詞的topic編號z_{m,n}\\
\end{split}
$$

---

$$
\begin{split}
&\vec{\beta} \rightarrow \vec{\varphi_k} \rightarrow w_{m,n}|k=z_{m,n} : 這個過程表示如何\\
&生成第m篇文檔的第n個詞。從第二個罈子抽出K個骰子，\\
&其中的第k=z_{m,n}個骰子作為這個詞的topic-word\\
&骰子\vec{\varphi_k}，然後投擲這個骰子生成文檔中第n個詞w_{m,n}
\end{split}
$$

---
$$
\vec{\alpha} \underbrace{\longrightarrow}_{Dirichlet} \vec{\theta_m} \underbrace\longrightarrow_{Multinomial} \vec{z_m}
$$

---


$$
\begin{split}
&p(\vec{z_m}|\vec{\alpha})=\frac{\Delta(\vec{n_m}+\vec{\alpha})}{\Delta\vec{\alpha}}\\
&其中\vec{n_m}=(n_m^{(1)},...,n_m^{(K)})，n_m^{(k)}表示第m篇文檔中\\
&第k個topic產生的詞的個數
\end{split}
$$

---

$$
\begin{split}
p(\vec{z}|\vec{\alpha})&=\prod_{m=1}^{M}p(\vec{z_m}|\vec{\alpha})\\
&=\prod_{m=1}^{M}\frac{\Delta(\vec{n_m}+\vec{\alpha})}{\Delta\vec{\alpha}}\\
\end{split}
$$

---

$$
\vec{\beta} \underbrace{\longrightarrow}_{Dirichlet} \vec{\varphi_k} \underbrace\longrightarrow_{Multinomial} \vec{w_{(k)}}
$$

---

$$
\begin{split}
&p(\vec{w_{(k)}}|\vec{\beta})=\frac{\Delta(\vec{n_k}+\vec{\beta})}{\Delta\vec{\beta}}\\
&其中\vec{n_k}=(n_k^{(1)},...,n_k^{(K)})，n_k^{(t)}表示第k個topic產生的詞中\\
&word\ t 的個數
\end{split}
$$

---

$$
\begin{split}
p(\vec{w}|\vec{z},\vec{\beta})&=\prod_{k=1}^{K}p(\vec{w_{(k)}}|\vec{z_{(k)},\beta})\\
&=\prod_{k=1}^{K}\frac{\Delta(\vec{n_k}+\vec{\beta})}{\Delta\vec{\beta}}\\
\end{split}
$$

---

$$
\begin{split}
p(\vec{w},\vec{z}|\vec{\alpha},\vec{\beta})&=p(\vec{w}|\vec{z},\vec{\beta})p(\vec{z}|\vec{\alpha})\\
&=\prod_{k=1}^{K}\frac{\Delta(\vec{n_k}+\vec{\beta})}{\Delta\vec{\beta}}\prod_{m=1}^{M}\frac{\Delta(\vec{n_m}+\vec{\alpha})}{\Delta\vec{\alpha}}\\
\end{split}
$$

---

$$
P(X_{t+1}=x|X_t,X_t-1,...)=P(X_{t+1}=x|X_t)
$$

---

$$
π_0P^n=πP=π
$$

---

$$
\begin{split}
&由於\vec{w}是觀測到的已知數據，只有\vec{z}是隱含的變量，\\
&所以我們真正需要採樣的是分布p(\vec{z}|\vec{w})。語料庫\vec{z}中\\
&的第i個詞對應的topic 我們記為z_i，其中i=(m,n)，\\
&表示第m篇文檔的第n個詞，我們用\neg i 表示去除下標為\\
&i的詞。那麼，按照Gibbs Sampling算法的要求，\\
&我們要求得任意座標軸i對應的條件分布\\
&p(z_i=k|\vec{z}_{\neg i},\vec{w})\\
&\\
&假設已觀測到的詞w_i=t，則由貝葉斯法則，\\
&可以得到\\
\end{split}
$$

---

$$
\begin{split}
p(z_i=k|\vec{z}_{\neg i},\vec{w}) &\propto p(z_i=k,w_i=t|\vec{z}_{\neg i},\vec{w}_{\neg i})\\
&=\int p(z_i=k,w_i=t,\vec{\theta}_m,\vec{\varphi}_k|\vec{z}_{\neg i},\vec{w}_{\neg i})d\vec{\theta}_md\vec{\varphi}_k\\
&...\\
&=\int \theta_{mk} Dir(\vec{\theta}_m|\vec{n}_{m,\neg i}+\vec{\alpha}) d \vec{\theta}_m 
\cdot \int \varphi_{kt} Dir(\vec{\varphi}_k|\vec{n}_{k,\neg i}+\vec{\beta})  d \vec{\varphi}_k\\
&=E(\theta_{mk}) \cdot E(\varphi_{kt})\\
&=\hat{\theta}_{mk} \cdot \hat{\varphi}_{kt}\\
\end{split}
$$

---

$$
\begin{split}
\hat{\theta}_{mk}&=\frac{n_{m,\neg i}^{(k)}+\alpha_k}{\sum_{k=1}^{K}(n_{m,\neg i}^{(k)}+\alpha_k)}\\
\hat{\varphi}_{kt}&=\frac{n_{k,\neg i}^{(t)}+\beta_t}{\sum_{t=1}^{V}(n_{k,\neg i}^{(t)}+\beta_t)}\\
\end{split}
$$

---

$$
\begin{split}
p(z_i=k|\vec{z}_{\neg i},\vec{w}) &\propto \underbrace{\frac{n_{m,\neg i}^{(k)}+\alpha_k}{\sum_{k=1}^{K}(n_{m,\neg i}^{(k)}+\alpha_k)}}_{p(topic|doc)} \cdot \underbrace{\frac{n_{k,\neg i}^{(t)}+\beta_t}{\sum_{t=1}^{V}(n_{k,\neg i}^{(t)}+\beta_t)}}_{p(word|topic)}\\
\end{split}
$$

---

