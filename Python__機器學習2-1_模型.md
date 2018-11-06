# Python__機器學習2-1_模型

[toc]
<!-- toc --> 

# scikit-learn

## API

- [API Reference — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.datasets)
    - [Choosing the right estimator — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/tutorial/machine_learning_map/index.html)
    - [Classifier comparison — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/auto_examples/classification/plot_classifier_comparison.html)


- [sklearn.preprocessing.MinMaxScaler — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MinMaxScaler.html)
    Transforms features by scaling each feature to a given range.

- [sklearn.preprocessing.StandardScaler — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)
    Standardize features by removing the mean and scaling to unit variance



- [scipy.sparse.csr_matrix — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.html)
    > Compressed Sparse Row matrix
    > 
    > __Advantages of the CSR format__
    > 
    > -   efficient arithmetic operations CSR + CSR, CSR * CSR, etc.
    > -   efficient row slicing
    > -   fast matrix vector products
    > 
    > __Disadvantages of the CSR format__
    > 
    > -   slow column slicing operations (consider CSC)
    > -   changes to the sparsity structure are expensive (consider LIL or DOK)

    - [scipy.sparse.csr_matrix.todense — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.todense.html#scipy.sparse.csr_matrix.todense)
        Return a dense matrix representation of this matrix.

    - [scipy.sparse.csr_matrix.toarray — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.toarray.html)
        Return a dense ndarray representation of this matrix.

    - [scipy.sparse.csr_matrix.sum — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.sum.html#scipy.sparse.csr_matrix.sum)
        Sum the matrix elements over a given axis.

- [sklearn.feature_extraction.text.CountVectorizer — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer)

    > Convert a collection of text documents to a matrix of token counts
    > 
    > This implementation produces a sparse representation of the counts using scipy.sparse.csr_matrix.
    > 
    > If you do not provide an a-priori dictionary and you do not use an analyzer that does some kind of feature selection then the number of features will be equal to the vocabulary size found by analyzing the data.

    - [sklearn.feature_extraction.text.CountVectorizer.fit_transform — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer.fit_transform)
        Learn the vocabulary dictionary and return term-document matrix.


    - [python - Can I use CountVectorizer in scikit-learn to count frequency of documents that were not used to extract the tokens? - Stack Overflow](https://stackoverflow.com/questions/22920801/can-i-use-countvectorizer-in-scikit-learn-to-count-frequency-of-documents-that-w)

        > You're right that `vocabulary` is what you want. It works like this:
        > 
        > ```
        > >>> cv = sklearn.feature_extraction.text.CountVectorizer(vocabulary=['hot', 'cold', 'old'])
        > >>> cv.fit_transform(['pease porridge hot', 'pease porridge cold', 'pease porridge in the pot', 'nine days old']).toarray()
        > array([[1, 0, 0],
        >        [0, 1, 0],
        >        [0, 0, 0],
        >        [0, 0, 1]], dtype=int64)
        > ```
        > 
        > So you pass it a dict with your desired features as the keys.
        > 
        > If you used `CountVectorizer` on one set of documents and then you want to use the set of features from those documents for a new set, use the `vocabulary_` attribute of your original CountVectorizer and pass it to the new one. So in your example, you could do
        > 
        > ```
        > newVec = CountVectorizer(vocabulary=vec.vocabulary_)
        > ```
        > 
        > to create a new tokenizer using the vocabulary from your first one.

- [MemoryError · Issue #40 · scikit-learn-contrib/imbalanced-learn](https://github.com/scikit-learn-contrib/imbalanced-learn/issues/40)
    MemoryError while using toarray(), todense()
    > This simple solution to handle sparse data is simply to turn it to dense array as you see here:  
    > `File "C:\Python34\lib\site-packages\unbalanceddataset-0.1-py3.4.egg\unbalanced_dataset\utils.py", line 36, in concatenate return sp.vstack(l).todense()`
    > 
    > Unfortunately, this implementation is simply not suited to work with sparse data intelligently, and you you turn your (probably) massive sparse matrix of 500k and probably a few thousand columns, you run out of RAM.
    > 

### GridSearchCV

- [sklearn.model_selection.GridSearchCV — scikit-learn 0.20.0 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)

    > **return_train_score** : boolean, optional
    > 
    > If `False`, the `cv_results_` attribute will not include training scores.

- [python - Tabulate accuracy and mean for each fold in GridSearchCV from scikit-learn - Stack Overflow](https://stackoverflow.com/questions/40284613/tabulate-accuracy-and-mean-for-each-fold-in-gridsearchcv-from-scikit-learn)
    > 
    > First, you should not use `grid_scores_` anymore since it was deprecated in version **0.18** in favor of `cv_results_` attribute. The `grid_scores_` attribute will not be available from version **0.20**.
    > 
    > * * * * *
    > 
    > **Q°** : *Did I understand correctly, that the score.mean() is the mean of the accuracies?*
    > 
    > **A** : The attribute `cv_results_` actually returns a dictionnary of all the metrics you are looking for. Check this out : [`cv_result_`](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html).


### sklearn.cross_validation deprecated in favor of the model_selection module

- [sklearn.cross_validation deprecated in favor of the model_selection module · Issue #202 · udacity/machine-learning](https://github.com/udacity/machine-learning/issues/202)

    > In order to remove this warning you have to import `from sklearn.model_selection` instead of `from sklearn.cross_validation`.

## scikit learn videos

- [justmarkham/scikit-learn-videos: Jupyter notebooks from the scikit-learn video series](https://github.com/justmarkham/scikit-learn-videos)

## update scikit-learn code from Python2 to Python3

- [How to update your scikit-learn code for 2018](https://www.dataschool.io/how-to-update-your-scikit-learn-code-for-2018/)

## score matrics

### accuracy_score

- [sklearn.metrics中的评估方法介绍（accuracy_score, recall_score, roc_curve, roc_auc_score, confusion_matrix） - Cherzhoucheer的博客 - CSDN博客](https://blog.csdn.net/CherDW/article/details/55813071)


    > 分类准确率分数是指所有分类正确的百分比。分类准确率这一衡量分类器的标准比较容易理解，但是它不能告诉你响应值的潜在分布，并且它也不能告诉你分类器犯错的类型。
    > 
    > 形式：
    > ```
    > sklearn.metrics.accuracy_score(y_true, y_pred, normalize=True, sample_weight=None)
    > 
    > normalize：默认值为True，返回正确分类的比例；如果为False，返回正确分类的样本数
    > ```
    > 
    > 示例：
    > ```
    > >>>import numpy as np
    > >>>from sklearn.metrics import accuracy_score
    > >>>y_pred = [0, 2, 1, 3]
    > >>>y_true = [0, 1, 2, 3]
    > >>>accuracy_score(y_true, y_pred)
    > 0.5
    > >>>accuracy_score(y_true, y_pred, normalize=False)
    > 2
    > ```


### recall_score

- [sklearn.metrics中的评估方法介绍（accuracy_score, recall_score, roc_curve, roc_auc_score, confusion_matrix） - Cherzhoucheer的博客 - CSDN博客](https://blog.csdn.net/CherDW/article/details/55813071)


    > 召回率 =提取出的正确信息条数 /样本中的信息条数。通俗地说，就是所有准确的条目有多少被检索出来了。
    > 
    > 形式：
    > ```
    > klearn.metrics.recall_score(y_true, y_pred, labels=None, pos_label=1,average='binary', sample_weight=None)
    > 
    > 
    > 参数average : string, [None, 'micro', 'macro'(default), 'samples', 'weighted']
    > 
    > 将一个二分类matrics拓展到多分类或多标签问题时，我们可以将数据看成多个二分类问题的集合，每个类都是一个二分类。接着，我们可以通过跨多个分类计算每个二分类metrics得分的均值，这在一些情况下很有用。你可以使用average参数来指定。
    > 
    > macro：计算二分类metrics的均值，为每个类给出相同权重的分值。当小类很重要时会出问题，因为该macro-averging方法是对性能的平均。另一方面，该方法假设所有分类都是一样重要的，因此macro-averaging方法会对小类的性能影响很大。
    > 
    > weighted:对于不均衡数量的类来说，计算二分类metrics的平均，通过在每个类的score上进行加权实现。
    > 
    > micro：给出了每个样本类以及它对整个metrics的贡献的pair（sample-weight），而非对整个类的metrics求和，它会每个类的metrics上的权重及因子进行求和，来计算整个份额。Micro-averaging方法在多标签（multilabel）问题中设置，包含多分类，此时，大类将被忽略。
    > 
    > samples：应用在multilabel问题上。它不会计算每个类，相反，它会在评估数据中，通过计算真实类和预测类的差异的metrics，来求平均（sample_weight-weighted）
    > 
    > average：average=None将返回一个数组，它包含了每个类的得分.
    > ```
    > 
    > 示例：
    > ```
    > >>>from sklearn.metrics import recall_score
    > >>>y_true = [0, 1, 2, 0, 1, 2]
    > >>>y_pred = [0, 2, 1, 0, 0, 1]
    > >>>recall_score(y_true, y_pred, average='macro')
    > 0.33...
    > >>>recall_score(y_true, y_pred, average='micro')
    > 0.33...
    > >>>recall_score(y_true, y_pred, average='weighted')
    > 0.33...
    > >>>recall_score(y_true, y_pred, average=None)
    > array([1.,  0., 0.])
    > ```
    > 

### roc_curve

- [sklearn.metrics.roc_curve — scikit-learn 0.20.0 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_curve.html)

- [sklearn.metrics中的评估方法介绍（accuracy_score, recall_score, roc_curve, roc_auc_score, confusion_matrix） - Cherzhoucheer的博客 - CSDN博客](https://blog.csdn.net/CherDW/article/details/55813071)



    > ROC曲线指受试者工作特征曲线/接收器操作特性(receiver operating characteristic，ROC)曲线,是反映灵敏性和特效性连续变量的综合指标,是用构图法揭示敏感性和特异性的相互关系，它通过将连续变量设定出多个不同的临界值，从而计算出一系列敏感性和特异性。ROC曲线是根据一系列不同的二分类方式（分界值或决定阈），以真正例率（也就是灵敏度）（True Positive Rate,TPR）为纵坐标，假正例率（1-特效性）（False Positive Rate,FPR）为横坐标绘制的曲线。
    > 
    > ROC观察模型正确地识别正例的比例与模型错误地把负例数据识别成正例的比例之间的权衡。TPR的增加以FPR的增加为代价。ROC曲线下的面积是模型准确率的度量，AUC（Area under roccurve）。
    > 
    > 纵坐标：真正率（True Positive Rate , TPR）或灵敏度（sensitivity）
    > 
    > TPR = TP /（TP + FN）  （正样本预测结果数 / 正样本实际数）
    > 
    > 横坐标：假正率（False Positive Rate , FPR）
    > 
    > FPR = FP /（FP + TN） （被预测为正的负样本结果数 /负样本实际数）
    > 
    > 形式：
    > ```
    > sklearn.metrics.roc_curve(y_true,y_score, pos_label=None, sample_weight=None, drop_intermediate=True)
    > 
    > 该函数返回这三个变量：fpr,tpr,和阈值thresholds;
    > 
    > 这里理解thresholds:
    > 
    > 分类器的一个重要功能"概率输出"，即表示分类器认为某个样本具有多大的概率属于正样本（或负样本）。
    > 
    > "Score"表示每个测试样本属于正样本的概率。
    > ```
    > 
    > 接下来，我们从高到低，依次将"Score"值作为阈值threshold，当测试样本属于正样本的概率大于或等于这个threshold时，我们认为它为正样本，否则为负样本。每次选取一个不同的threshold，我们就可以得到一组FPR和TPR，即ROC曲线上的一点。当我们将threshold设置为1和0时，分别可以得到ROC曲线上的(0,0)和(1,1)两个点。将这些(FPR,TPR)对连接起来，就得到了ROC曲线。当threshold取值越多，ROC曲线越平滑。其实，我们并不一定要得到每个测试样本是正样本的概率值，只要得到这个分类器对该测试样本的"评分值"即可（评分值并不一定在(0,1)区间）。评分越高，表示分类器越肯定地认为这个测试样本是正样本，而且同时使用各个评分值作为threshold。我认为将评分值转化为概率更易于理解一些。
    > 
    > 示例：
    > ```
    > >>>import numpy as np
    > >>>from sklearn import metrics
    > >>>y = np.array([1, 1, 2, 2])
    > >>>scores = np.array([0.1, 0.4, 0.35, 0.8])
    > >>>fpr, tpr, thresholds = metrics.roc_curve(y, scores, pos_label=2)
    > >>>fpr
    > array([0. ,  0.5,  0.5, 1. ])
    > >>>tpr
    > array([0.5,  0.5,  1. , 1. ])
    > >>>thresholds
    > array([0.8 ,  0.4 ,  0.35, 0.1 ])
    > >>>from sklearn.metrics import auc
    > >>>metrics.auc(fpr, tpr)
    > 0.75
    > ```
    > 


### roc_auc_score

- [sklearn.metrics.roc_auc_score — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_auc_score.html#sklearn.metrics.roc_auc_score)

- [sklearn.metrics中的评估方法介绍（accuracy_score, recall_score, roc_curve, roc_auc_score, confusion_matrix） - Cherzhoucheer的博客 - CSDN博客](https://blog.csdn.net/CherDW/article/details/55813071)


    > 直接根据真实值（必须是二值）、预测值（可以是0/1,也可以是proba值）计算出auc值，中间过程的roc计算省略。
    > 
    > 形式：
    > ```
    > sklearn.metrics.roc_auc_score(y_true, y_score, average='macro', sample_weight=None)
    > 
    > average : string, [None, ‘micro’, ‘macro’(default), ‘samples’, ‘weighted’]
    > ```
    > 
    > 示例：
    > ```
    > >>>import numpy as np
    > >>>from sklearn.metrics import roc_auc_score
    > >>>y_true = np.array([0, 0, 1, 1])
    > >>>y_scores = np.array([0.1, 0.4, 0.35, 0.8])
    > >>>roc_auc_score(y_true, y_scores)
    > 0.75
    > ```


### confusion_matrix

- [sklearn.metrics中的评估方法介绍（accuracy_score, recall_score, roc_curve, roc_auc_score, confusion_matrix） - Cherzhoucheer的博客 - CSDN博客](https://blog.csdn.net/CherDW/article/details/55813071)

    > 
    > 
    > 用一个例子来理解混淆矩阵：
    > 
    > 假设有一个用来对猫（cats）、狗（dogs）、兔子（rabbits）进行分类的系统，混淆矩阵就是为了进一步分析性能而对该算法测试结果做出的总结。假设总共有 27 只动物：8只猫， 6条狗， 13只兔子。结果的混淆矩阵如下图：
    > 
    > ![](https://i.imgur.com/DRs3oqX.jpg)
    > 
    > 在这个混淆矩阵中，实际有 8只猫，但是系统将其中3只预测成了狗；对于 6条狗，其中有 1条被预测成了兔子，2条被预测成了猫。从混淆矩阵中我们可以看出系统对于区分猫和狗存在一些问题，但是区分兔子和其他动物的效果还是不错的。所有正确的预测结果都在对角线上，所以从混淆矩阵中可以很方便直观的看出哪里有错误，因为他们呈现在对角线外面。
    > 
    > 形式：
    > ```
    > sklearn.metrics.confusion_matrix(y_true, y_pred, labels=None, sample_weight=None)
    > 
    > 返回一个混淆矩阵；
    > 
    > labels：混淆矩阵的索引（如上面猫狗兔的示例），如果没有赋值，则按照y_true, y_pred中出现过的值排序。
    > ```
    > 
    > 示例：
    > ```
    > >>>from sklearn.metrics import confusion_matrix
    > >>>y_true = [2, 0, 2, 2, 0, 1]
    > >>>y_pred = [0, 0, 2, 2, 0, 2]
    > >>>confusion_matrix(y_true, y_pred)
    > array([[2,0, 0],
    >        [0, 0, 1],
    >        [1, 0, 2]])
    > 
    > >>>y_true = ["cat", "ant", "cat", "cat","ant", "bird"]
    > >>>y_pred = ["ant", "ant", "cat", "cat","ant", "cat"]
    > >>>confusion_matrix(y_true, y_pred, labels=["ant", "bird","cat"])
    > array([[2,0, 0],
    >        [0, 0, 1],
    >        [1, 0, 2]])
    > ```
    > 



## Model select/Cross Validation

- [API Reference — scikit-learn 0.20.0 documentation](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.model_selection)

- [API Reference — scikit-learn 0.17 文档](https://lijiancheng0614.github.io/scikit-learn/modules/classes.html#module-sklearn.cross_validation)

- [3.1. Cross-validation: evaluating estimator performance — scikit-learn 0.20.0 documentation](http://scikit-learn.org/stable/modules/cross_validation.html#cross-validation)

### Train/Test/Validation Set Splitting

- [machine learning - Train/Test/Validation Set Splitting in Sklearn - Data Science Stack Exchange](https://datascience.stackexchange.com/questions/15135/train-test-validation-set-splitting-in-sklearn)

    > You could just use `sklearn.model_selection.train_test_split` twice. First to split to train, test and then split train again into validation and train. Something like this:
    > 
    > ```
    >  X_train, X_test, y_train, y_test
    >     = train_test_split(X, y, test_size=0.2, random_state=1)
    > 
    >  X_train, X_val, y_train, y_val
    >     = train_test_split(X_train, y_train, test_size=0.2, random_state=1)
    > 
    > ```

## Model Tuning

### Grid search

- [Scanning hyperspace: how to tune machine learning models | Cambridge Coding Academy](https://cambridgecoding.wordpress.com/2016/04/03/scanning-hyperspace-how-to-tune-machine-learning-models/)


    > Grid search
    > -----------
    > 
    > Traditionally and perhaps most intuitively, scanning for good HPs values can be done with **grid search** (also called parameter sweep). This strategy exhaustively searches through some manually prespecified HP values and reports the best option. It is common to try to optimize multiple HPs simultaneously -- grid search tries each combination of HPs in turn and reports the best one, hence the name 'grid'. This is a more convenient and complete way of searching through hyperparameter space than manually specifying combinations.
    > 
    > For instance, you could build a grid like this:
    > 
    > [![grid_search](https://cambridgecoding.files.wordpress.com/2016/04/grid_search1.png?w=450&h=383)](https://cambridgecoding.files.wordpress.com/2016/04/grid_search1.png)
    > 
    > Using these commands:
    > 
    > ```python
    > import itertools
    >  
    > n_estimators = [2, 5, 9]
    > max_features = [None, 'log2', 'sqrt']
    >  
    > hp_combinations = list(itertools.product(n_estimators, max_features))
    > print (hp_combinations)
    > print ("The number of HP combinations is: {}".format(len(hp_combinations)))
    > ```
    > 
    > ```
    > [(2, None), (2, 'log2'), (2, 'sqrt'), (5, None), (5, 'log2'), (5, 'sqrt'), (9, None), (9, 'log2'), (9, 'sqrt')]
    > The number of HP combinations is: 9
    > 
    > ```
    > 
    > However there is a **massive pitfall** here! Scanning through all possible combinations of HPs to build models and evaluating them on the test set will output the combination of parameters that does best, but these values might not generalise well. This approach is less misguided than trying to optimize models by evaluating them on the training set, but is still not ideal. The problem is that during repeated evaluation on the test dataset, knowledge of the test set can leak into the model building phase. You are at risk of inadvertently learning something about the test set, and hence are susceptible to [**overfitting**](http://blog.cambridgecoding.com/2016/03/24/misleading-modelling-overfitting-cross-validation-and-the-bias-variance-trade-off/). How does one get around these issues?
    > 
    > Grid search with k-fold cross validation for hyperparameter tuning
    > ------------------------------------------------------------------
    > 
    > Enter **k-fold cross-validation**, which is a handy technique for measuring a model's performance using *only* the training set. k-fold CV is a general method (see an explanation [here](http://blog.cambridgecoding.com/2016/03/24/misleading-modelling-overfitting-cross-validation-and-the-bias-variance-trade-off/)), and is not specific to hyperparameter optimization, but is very useful for that purpose. You simply try out different HP values, get several different estimates of model performance for each HP value (or combination of HP values), and choose the model with the lowest CV error. With 10-fold CV, the process looks like this:
    > 
    > [![Diagram showing the steps behind 10-fold cross-validation for hyperparameter optimization.](https://cambridgecoding.files.wordpress.com/2016/03/gridsearch_cv.png?w=610&h=406)](https://cambridgecoding.files.wordpress.com/2016/03/gridsearch_cv.png)
    > 
    > In the context of HP optimization, you perform k-fold cross validation **together with grid search** to get a more robust estimate of the model performance associated with specific HP values. The combination of grid search and k-fold cross validation is very popular for finding the models with good performance and generalisability. So, in HP optimisation, you are actually trying to do two things:
    > 
    > -   Find the combination of HPs that improves model performance (e.g. accuracy)
    > -   Make sure that this choice of HPs will generalize well to new data
    > 
    > The CV is there to address the second concern. `scikit-learn` makes grid search with k-fold CV very easy and slick to do, and even supports parallel distributing of the search (via the `n_jobs` argument). The set-up looks like this:
    > 
    > ```python
    > from sklearn.grid_search import GridSearchCV
    >  
    > # Search for good hyperparameter values
    > # Specify values to grid search over
    > n_estimators = list(np.arange(10, 60, 20))
    > max_features = [None, 'sqrt', 'log2'] 
    >  
    > hyperparameters = {
    >     'n_estimators': n_estimators, 
    >     'max_features': max_features
    > }
    >  
    > # Grid search using cross-validation
    > gridCV = GridSearchCV(RandomForestClassifier(), param_grid=hyperparameters, cv=10, n_jobs=4)
    > ```
    > 
    > Next, you tell the model to use the training data to perform the grid search with 10 fold CV. You can then collect the best combination of HP values with the model attribute `best_params_`:
    > 
    > ```python
    > # Perform grid search with 10-fold CV
    > gridCV.fit(XTrain, yTrain)
    >  
    > # Identify optimal hyperparameter values
    > best_n_estim      = gridCV.best_params_['n_estimators']
    > best_max_features = gridCV.best_params_['max_features']  
    >  
    > print("The best performing n_estimators value is: {}".format(best_n_estim))
    > print("The best performing max_features value is: {}".format(best_max_features))
    > ```
    > 
    > ```
    > The best performing n_estimators value is: 30
    > The best performing max_features value is: sqrt
    > 
    > ```
    > 
    > You can visually represent the results from this grid search (stored in `gridCV.grid_scores_`) with a heatmap:
    > 
    > ```python
    > import matplotlib.pyplot as plt
    > %matplotlib inline
    >  
    > # fetch scores, reshape into a grid
    > scores = [x[1] for x in gridCV.grid_scores_]
    > scores = np.array(scores).reshape(len(n_estimators), len(max_features))
    > scores = np.transpose(scores)
    >  
    > # Make heatmap from grid search results
    > plt.figure(figsize=(12, 6))
    > plt.imshow(scores, interpolation='nearest', origin='higher', cmap='jet_r')
    > plt.xticks(np.arange(len(n_estimators)), n_estimators)
    > plt.yticks(np.arange(len(max_features)), max_features)
    > plt.xlabel('Number of decision trees')
    > plt.ylabel('Max features')
    > plt.colorbar().set_label('Classification Accuracy', rotation=270, labelpad=20)
    > plt.show()
    > ```
    > 
    > [![heatmap_grid_CV](https://cambridgecoding.files.wordpress.com/2016/03/heatmap_grid_cv.png?w=610)](https://cambridgecoding.files.wordpress.com/2016/03/heatmap_grid_cv.png)
    > 
    > Finally, you can now train a new random forest on the wine dataset using what you have learned from the grid search:
    > 
    > ```python
    > # Train classifier using optimal hyperparameter values
    > # You could have also gotten this model out from gridCV.best_estimator_
    > rf = RandomForestClassifier(n_estimators=best_n_estim,
    >                             max_features=best_max_features)
    >  
    > rf.fit(XTrain, yTrain)
    > rf_predictions = rf.predict(XTest)
    >  
    > print (metrics.classification_report(yTest, rf_predictions))
    > print ("Overall Accuracy:", round(metrics.accuracy_score(yTest, rf_predictions),2))
    > ```
    > 
    > ```
    >              precision    recall  f1-score   support
    > 
    >         0.0       0.79      0.84      0.81       188
    >         1.0       0.84      0.80      0.82       212
    > 
    > avg / total       0.82      0.81      0.82       400
    > 
    > ('Overall Accuracy:', 0.81)
    > 
    > ```
    > 
    > Congratulations, you tuned and applied your random forest classifier! You now get ~0.81 accuracy. This is quite a bit better than the poorly parameterized models which yielded ~0.7 accuracy, and is a noticeable difference from the default 0.77-0.79 values. Importantly, it was not too difficult to get this boost -- scikit can do grid search with k-fold CV in 1 line of code. How could you try to improve performance further?
    > 
    > Note that grid search with k-fold CV simply returns the best HP values out of the available options, and is therefore not guaranteed to return a global optimum. It makes sense to choose a diverse collection of possible values that is somewhat centred around an empirically sensible default.
    > 


## Models

### PCA

- [sklearn.decomposition.PCA — scikit-learn 0.20.0 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)



# PCA

- [PCA(主成分分析)python实现 - 简书](https://www.jianshu.com/p/4528aaa6dc48)


# XGBoost

- [XGBoost 与 Boosted Tree – 我爱计算机](http://www.52cs.org/?p=429)

- [Complete Guide to Parameter Tuning in XGBoost (with codes in Python)](https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/)

- [[1603.02754] XGBoost: A Scalable Tree Boosting System](https://arxiv.org/abs/1603.02754)



## Mathematics Behind XGBoost

- [Unveiling Mathematics Behind XGBoost](https://www.kdnuggets.com/2018/08/unveiling-mathematics-behind-xgboost.html)

    > ### **Curious case of John and Emily**
    > ![](https://cdn-images-1.medium.com/max/720/1*mWtNfyZwXju3-tZfRFYcng.jpeg)
    > 
    > John and Emily embarked on an adventure to pluck apples from the tree located at the lowest point of the mountain. While Emily is a smart and adventurous girl, John is a bit cautious and sluggish. However, only John can climb tree and pluck apples. We will see how they achieve their goal.\
    > ![](https://cdn-images-1.medium.com/max/720/1*LA8TV-PCjh1on6MQ1LxOVw.jpeg)
    > 
    > John and Emily start at point 'a' on the mountain and tree is located at point 'g'. There are two ways they can reach point 'g':
    > 
    > 1\. Emily calculates the slope of the curve at point 'a'; if the slope is positive, they move in the opposite direction or else in the same direction. However, slope gives direction but doesn't tell how much they need to move in that direction. Therefore, Emily decides to take small step and repeat the process, so they don't end up at the wrong point. While the direction of the step is controlled by the negative gradient, the magnitude of the step is controlled by the learning rate. If the magnitude is either too high or too low, they may end up at a wrong point or take way too long to reach to point 'g'.\
    > ![](https://cdn-images-1.medium.com/max/720/1*wQXYeg4Jrvb-4a3Nz4SP7w.jpeg)
    > 
    > John is skeptical about this approach and doesn't want to walk more if by chance they end up at the wrong point. So Emily comes up with a new approach:
    > 
    > 2\. Emily suggests that she will first go to next potential points and calculate the value of the loss function at those points. She keeps a note of the value of the function at all those points, and she will signal John to come to that point where the value is least. John loved this approach as he will never end up at a wrong point. However, poor Emily need to explore all points in her neighborhood and calculate the value of the function at all those points. The beauty of XGBoost is it intelligently tackles both these problems.
    > 
    > Please be advised I may use function/base learner/tree interchangeably.
    > 
    > ### **Gradient Boosting**
    > Many implementations of Gradient Boosting follow approach 1 to minimize the objective function. At every iteration, we fit a base learner to the negative gradient of the loss function and multiply our prediction with a constant and add it to the value from previous iteration.
    > 
    > ![](https://cdn-images-1.medium.com/max/720/1*Ghv8bGUk0zzYfUouEJYuyw.png)\
    > [Source: Wikipedia](https://en.wikipedia.org/wiki/Gradient_boosting)
    > 
    > The intuition is by fitting a base learner to the negative gradient at each iteration is essentially performing gradient descent on the loss function. The negative gradients are often called as pseudo residuals, as they indirectly help us to minimize the objective function.
    > 
    > ### **XGBoost**
    > It was a result of research by Tianqi Chen, Ph.D. student at University of Washington. XGBoost is an ensemble additive model that is composed of several base learners.\
    > ![](https://cdn-images-1.medium.com/max/720/1*hyVH1RhJaDkDksy7_f4Ocw.jpeg)
    > 
    > How should we chose a function at each iteration? we chose a function that minimizes the overall loss.\
    > ![](https://cdn-images-1.medium.com/max/720/1*pzR03dxcSOhn2tnKtAXo3A.jpeg)
    > 
    > In the gradient boosting algorithm stated above, we obtained f~t~(x~i~) at each iteration by fitting a base learner to the negative gradient of loss function with respect to previous iteration's value. In XGBoost, we explore several base learners or functions and pick a function that minimizes the loss (Emily's second approach). As I stated above, there are two problems with this approach:\
    > 1\. exploring different base learners\
    > 2\. calculating the value of the loss function for all those base learners.
    > 
    > XGBoost uses Taylor series to approximate the value of the loss function for a base learner f~t~(x~i~), thus, reducing the load on Emily to calculate the exact loss for different possible base learners.\
    > ![](https://cdn-images-1.medium.com/max/720/1*TZDFiZ8EaBUbv8POwgAwcQ.jpeg)
    > 
    > It only uses expansion up to second order derivative assuming this level of approximation would be suffice. The first term 'C' is constant irrespective of any f~t~(x~i~) we pick. 'g~i~' is the first order derivative of loss at previous iteration with respect predictions at previous iteration. 'h~i~' is the second order derivative of loss at previous iteration with respect to predictions at previous iteration. Therefore, Emily can calculate 'g~i~' and 'f~i~' before starting exploring different base learners, as it will be just a matter of multiplications thereafter. Plug and play, isn't it?
    > 
    > So XGBoost has reduced one of the burdens on Emily. Still we have a problem of exploring different base learners.\
    > ![](https://cdn-images-1.medium.com/max/720/1*Sku1s6Y2NYyh71scMy8fSA.jpeg)
    > 
    > Assume Emily fixed a base learner ft that has 'K' leaf nodes. Let I~j~ be the set of instances belonging to node 'j' and 'w~j~' be the prediction for that node. So for an instance 'i' belonging to I~j~, f~t~(x~i~)=w~j~. Therefore, we obtained equation 3 from equation 2 by substituting f~t~(x~i~) with respective predictions. After substituting the predictions, we can take the derivative of loss function with respect to each leaf node's weight, to get an optimal weight.\
    > ![](https://cdn-images-1.medium.com/max/720/1*-tt8E0OzV2O2pKH6v5wMuQ.jpeg)
    > 
    > Substituting the optimal weights back into equation 3 gives equation 4. However, this is the optimal loss for a fixed tree structure. There will be several hundreds of possible trees.
    > 
    > Let's formulate the current position of Emily. She now knows how to ease the burden of computing loss using Taylor expansion. She knows for a fixed tree structure what should be the optimal weights in the leaf node. The only thing that is still a concern is how to explore all different possible tree structures.\
    > ![](https://cdn-images-1.medium.com/max/720/1*De1hXISG0y_7iL6OhxrJIw.jpeg)
    > 
    > Instead of exploring all possible tree structures, XGBoost greedily builds a tree. The split that results in maximum loss reduction is chosen. In the above picture, the tree starts at Node 'I'. Based on some split criteria, the node is divided into left and right branches. So some instances fall in left node and other instances fall in right leaf node. Now, we can calculate the reduction in loss and pick the split that causes best reduction in loss.
    > 
    > But still Emily has one more problem. How to chose the split criteria? XGBoost uses different tricks to come up with different split points like histogram, exact, etc. I will not be dealing with that part, as this article has already grown in size.\
    > **Bullet Points to Remember**
    > 
    > 1.  While Gradient Boosting follows negative gradients to optimize the loss function, XGBoost uses Taylor expansion to calculate the value of the loss function for different base learners. Here is the best video on the internet that explains [Taylor expansion](https://www.youtube.com/watch?v=3d6DsjIBzJ4&t=447s).
    > 2.  XGBoost doesn't explore all possible tree structures but builds a tree greedily.
    > 3.  XGBoost's regularization term penalizes building complex tree with several leaf nodes.
    > 4.  XGBoost has several other tricks under its sleeve like Column subsampling, shrinkage, splitting criteria, etc. I highly recommend continue reading the original paper [here](https://arxiv.org/pdf/1603.02754.pdf).
    > 
    > You can view the complete derivation [here](https://drive.google.com/open?id=1CmNhi-7pZFnCEOJ9g7LQXwuIwom0ZN_D).
    > 
    > Read my other article on PCA [here](https://www.linkedin.com/pulse/eigendecomposition-singular-value-decomposition-ajit-samudrala/).\
    > **Bio: [Ajit Samudrala](https://www.linkedin.com/in/ajitsamudrala/)** is an aspiring Data Scientist and Data Science intern at SiriusXM.
    > 
    > [Original](https://medium.com/@samudralaajit/unveiling-mathematics-behind-xgboost-c7f1b8201e2a). Reposted with permission.
    > 


## Leaf Encoding

- [predicting-clicks-facebook.pdf](http://quinonero.net/Publications/predicting-clicks-facebook.pdf)

- [Python API Reference — xgboost 0.7 documentation](https://xgboost.readthedocs.io/en/latest/python/python_api.html#module-xgboost.sklearn)

    ![](https://screenshotscdn.firefoxusercontent.com/images/4eb1256c-81e9-4c91-af15-d5325f57f5c8.png)

## What does the value of 'leaf' in the following xgboost model tree diagram means

- [python - What does the value of 'leaf' in the following xgboost model tree diagram means? - Stack Overflow](https://stackoverflow.com/questions/40926340/what-does-the-value-of-leaf-in-the-following-xgboost-model-tree-diagram-means)

    > For a classification tree with 2 classes {0,1}, the value of the leaf node represent the raw score for class 1. It can be converted to a probability score by using the logistic function. The calculation below use the left most leaf as an example.
    > 
    > ```
    > 1/(1+np.exp(-1*0.167528))=0.5417843204057448
    > ```
    > 
    > What this means is if a data point ends up being distributed to this leaf, the probability of this data point being class 1 is 0.5417843204057448.

## how to interpret the dump of xgboost's tree model

- [how to interpret the dump of xgboost's tree model | Kaggle](https://www.kaggle.com/general/20322)

    > Predictions are made by summing up the corresponding leaf values of each tree. Additionally, you need to transform those values depending on the objective you have choosen. For instance: If you trained your xgb with binary:logistic, the sum of the leaf values will be the logit score. So you need to apply the logistic function to get the wanted probabilities.


## How to Visualize Gradient Boosting Decision Trees With XGBoost in Python

- [How to Visualize Gradient Boosting Decision Trees With XGBoost in Python](https://machinelearningmastery.com/visualize-gradient-boosting-decision-trees-xgboost-python/)

    > ```python
    > # plot decision tree
    > from numpy import loadtxt
    > from xgboost import XGBClassifier
    > from xgboost import plot_tree
    > import matplotlib.pyplot as plt
    > # load data
    > dataset = loadtxt('pima-indians-diabetes.csv', delimiter=",")
    > # split data into X and y
    > X = dataset[:,0:8]
    > y = dataset[:,8]
    > # fit model no training data
    > model = XGBClassifier()
    > model.fit(X, y)
    > # plot single tree
    > plot_tree(model)
    > plt.show()
    > ```
    > Running the code creates a plot of the first decision tree in the model (index 0), showing the features and feature values for each split as well as the output leaf nodes.
    > 
    > ![XGBoost Plot of Single Decision Tree](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2016/07/XGBoost-Plot-of-Single-Decision-Tree.png)
    > 
    > 
    > You can also change the layout of the graph to be left to right (easier to read) by changing the **rankdir** argument as 'LR' (left-to-right) rather than the default top to bottom (UT). For example:
    > ```
    > plot_tree(model, num_trees=0, rankdir='LR')
    > ```
    > 
    > The result of plotting the tree in the left-to-right layout is shown below.
    > 
    > ![XGBoost Plot of Single Decision Tree Left-To-Right](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2016/07/XGBoost-Plot-of-Single-Decision-Tree-Left-To-Right.png)
    > 

## Evaluate XGBoost Models With Learning Curves

- [Avoid Overfitting By Early Stopping With XGBoost In Python](https://machinelearningmastery.com/avoid-overfitting-by-early-stopping-with-xgboost-in-python/)

    > ```python
    > # plot learning curve
    > from numpy import loadtxt
    > from xgboost import XGBClassifier
    > from sklearn.model_selection import train_test_split
    > from sklearn.metrics import accuracy_score
    > from matplotlib import pyplot
    > # load data
    > dataset = loadtxt('pima-indians-diabetes.csv', delimiter=",")
    > # split data into X and y
    > X = dataset[:,0:8]
    > Y = dataset[:,8]
    > # split data into train and test sets
    > X_train, X_test, y_train, y_test = train_test_split(X, Y, test_size=0.33, random_state=7)
    > # fit model no training data
    > model = XGBClassifier()
    > eval_set = [(X_train, y_train), (X_test, y_test)]
    > model.fit(X_train, y_train, eval_metric=["error", "logloss"], eval_set=eval_set, verbose=True)
    > # make predictions for test data
    > y_pred = model.predict(X_test)
    > predictions = [round(value) for value in y_pred]
    > # evaluate predictions
    > accuracy = accuracy_score(y_test, predictions)
    > print("Accuracy: %.2f%%" % (accuracy * 100.0))
    > # retrieve performance metrics
    > results = model.evals_result()
    > epochs = len(results['validation_0']['error'])
    > x_axis = range(0, epochs)
    > # plot log loss
    > fig, ax = pyplot.subplots()
    > ax.plot(x_axis, results['validation_0']['logloss'], label='Train')
    > ax.plot(x_axis, results['validation_1']['logloss'], label='Test')
    > ax.legend()
    > pyplot.ylabel('Log Loss')
    > pyplot.title('XGBoost Log Loss')
    > pyplot.show()
    > # plot classification error
    > fig, ax = pyplot.subplots()
    > ax.plot(x_axis, results['validation_0']['error'], label='Train')
    > ax.plot(x_axis, results['validation_1']['error'], label='Test')
    > ax.legend()
    > pyplot.ylabel('Classification Error')
    > pyplot.title('XGBoost Classification Error')
    > pyplot.show()
    > ```
    > 
    > Two plots are created. The first shows the logarithmic loss of the XGBoost model for each epoch on the training and test datasets.
    > 
    > ![XGBoost Learning Curve Log Loss](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2016/07/XGBoost-Learning-Curve-Log-Loss.png)
    > 
    > XGBoost Learning Curve Log Loss
    > 
    > The second plot shows the classification error of the XGBoost model for each epoch on the training and test datasets.
    > 
    > ![XGBoost Learning Curve Classification Error](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2016/07/XGBoost-Learning-Curve-Classification-Error.png)
    > 
    > XGBoost Learning Curve Classification Error
    > 
    > From reviewing the logloss plot, it looks like there is an opportunity to stop the learning early, perhaps somewhere around epoch 20 to epoch 40.
    > 

## Save model & load model

### save model by Pickle 

- [How to Save Gradient Boosting Models with XGBoost in Python - Machine Learning Mastery](https://machinelearningmastery.com/save-gradient-boosting-models-xgboost-python/)

    > Serialize Your XGBoost Model with Pickle
    > ----------------------------------------
    > 
    > Pickle is the standard way of serializing objects in Python.
    > 
    > You can use the [Python pickle API](https://docs.python.org/2/library/pickle.html) to serialize your machine learning algorithms and save the serialized format to a file, for example:


    > ```python
    > # Train XGBoost model, save to file using pickle, load and make predictions
    > from numpy import loadtxt
    > import xgboost
    > import pickle
    > from sklearn import model_selection
    > from sklearn.metrics import accuracy_score
    > # load data
    > dataset = loadtxt('pima-indians-diabetes.csv', delimiter=",")
    > # split data into X and y
    > X = dataset[:,0:8]
    > Y = dataset[:,8]
    > # split data into train and test sets
    > seed = 7
    > test_size = 0.33
    > X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, Y, test_size=test_size, random_state=seed)
    > # fit model no training data
    > model = xgboost.XGBClassifier()
    > model.fit(X_train, y_train)
    > # save model to file
    > pickle.dump(model, open("pima.pickle.dat", "wb"))
    > 
    > # some time later...
    > 
    > # load model from file
    > loaded_model = pickle.load(open("pima.pickle.dat", "rb"))
    > # make predictions for test data
    > y_pred = loaded_model.predict(X_test)
    > predictions = [round(value) for value in y_pred]
    > # evaluate predictions
    > accuracy = accuracy_score(y_test, predictions)
    > print("Accuracy: %.2f%%" % (accuracy * 100.0))
    > ```

### restore both model and feature names
- [How to restore both model and feature names · Issue #3089 · dmlc/xgboost](https://github.com/dmlc/xgboost/issues/3089)

    > Other than pickling, you can also store any model metadata you want in a string key-value form within its binary contents by using the internal (not python) booster attributes.\
    > E.g., to create an internal 'feature_names' attribute before calling save_model, do
    > 
    > ```source-python
    > if hasattr(bst, 'feature_names'): bst.set_attr(feature_names = '|'.join(bst.feature_names))
    > ```
    > 
    > Then after loading that model you may restore the python 'feature_names' attribute:
    > 
    > ```source-python
    > if bst.attr('feature_names') is not None: bst.feature_names = bst.attr('feature_names').split('|')
    > ```

## Feature

### How to get feature importance in xgboost

- [python - How to get feature importance in xgboost? - Stack Overflow](https://stackoverflow.com/questions/37627923/how-to-get-feature-importance-in-xgboost)

    > Build the model from XGboost first
    > 
    > ```
    > from xgboost import XGBClassifier, plot_importance
    > model = XGBClassifier()
    > model.fit(train, label)
    > ```
    > 
    > this would result in an array. So we can sort it with descending
    > 
    > ```
    > sorted_idx = np.argsort(model.feature_importances_)[::-1]
    > ```
    > 
    > Then, it is time to print all sorted importances and the name of columns together as lists (I assume the data loaded with Pandas)
    > 
    > ```
    > for index in sorted_idx:
    >     print([train.columns[index], model.feature_importances_[index]])
    > ```
    > 
    > * * * * *
    > 
    > Furthermore, we can plot the importances with XGboost built-in function
    > 
    > ```
    > plot_importance(model, max_num_features = 15)
    > pyplot.show()
    > ```
    > 
    > use `max_num_features` in `plot_importance` to limit the number of features if you want.
    > 


### Far0n/xgbfi: XGBoost Feature Interactions & Importance

- [Far0n/xgbfi: XGBoost Feature Interactions & Importance](https://github.com/Far0n/xgbfi)

    > Xgbfi is a XGBoost model dump parser, which ranks features as well as feature interactions by different metrics.
    > 
    > ### The Metrics
    > 
    > -   **Gain**: Total gain of each feature or feature interaction
    > -   **FScore**: Amount of possible splits taken on a feature or feature interaction
    > -   **wFScore**: Amount of possible splits taken on a feature or feature interaction weighted by the probability of the splits to take place
    > -   **Average wFScore**: *wFScore* divided by *FScore*
    > -   **Average Gain**: *Gain* divided by *FScore*
    > -   **Expected Gain**: Total gain of each feature or feature interaction weighted by the probability to gather the gain
    > -   **Average Tree Index**
    > -   **Average Tree Depth**


## Win10下XGBoost安装方法

- [Win10下XGBoost安装方法(本地python3.5和anaconda版) | Code my word](https://denotepython.github.io/2017/03/11/install-xgboost/)

    > 下载xgboost.whl
    > -------------
    > 
    > 因为现在已经出了xgboost的whl版本，所以安装变得十分便捷，首先去[xgboost whl](http://www.lfd.uci.edu/~gohlke/pythonlibs/#xgboost)下载自己对应的版本，我的是`xgboost‑0.6‑cp35‑cp35m‑win_amd64.whl`然后放到任意目录，比如我放到G盘根目录
    > 
    > anaconda安装xgboost
    > -----------------
    > 
    > 首先切换到anaconda下你安装的python3.5版本的目录，因为我是创建的虚拟环境，所以在env目录下 
    > `C:\Users\rocket\Anaconda2\envs\python35\Scripts>` 
    > 切换成功过后，同样输入`pip install G:\xgboost-0.6-cp35-cp35m-win_amd64.whl` 
    > 
    > ```shell
    > Processing g:\xgboost-0.6-cp35-cp35m-win_amd64.whl
    > Requirement already satisfied: scipy in c:\\users\rocket\anaconda2\envs\python35\lib\site-packages (from xgboost==0.6)
    > Requirement already satisfied: numpy in c:\users\rocket\anaconda2\envs\python35\lib\site-packages (from xgboost==0.6)
    > Installing collected packages: xgboost
    > Successfully installed xgboost-0.6
    > ```


# CatBoost

- [CatBoost — Transforming categorical features to numerical features — Yandex Technologies](https://tech.yandex.com/catboost/doc/dg/concepts/algorithm-main-stages_cat-to-numberic-docpage/)

內建 Mean Encoding = Target Encoding



# Hierarchical Clustering

- [利用 SciPy 实现层次聚类 - Haojun's Blog](https://haojunsui.github.io/2016/07/16/scipy-hac/)

# HDBscan

## API

- [Comparing Python Clustering Algorithms — hdbscan 0.8.1 documentation](https://hdbscan.readthedocs.io/en/latest/comparing_clustering_algorithms.html)