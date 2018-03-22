# Keras__深度學習

## API reference

- [Sequential - Keras Documentation](https://keras.io/models/sequential/)

- keras.layers
    - [Core Layers - Keras Documentation](https://keras.io/layers/core/)

- [Losses - Keras Documentation](https://keras.io/losses/#available-loss-functions)

- [Initializers - Keras Documentation](https://keras.io/initializers/)

- [Optimizers - Keras Documentation](https://keras.io/optimizers/)

- [Metrics - Keras Documentation](https://faroit.github.io/keras-docs/1.1.1/metrics/)


## tutorial

- [Guide to the Sequential model - Keras Documentation](https://keras.io/getting-started/sequential-model-guide/#compilation)


## Usage


### Model Save & Reload
- [Save & reload 保存提取 - Keras | 莫烦Python](https://morvanzhou.github.io/tutorials/machine-learning/keras/3-1-save/)



    > 保存模型[](https://morvanzhou.github.io/tutorials/machine-learning/keras/3-1-save/#保存模型 "Permalink to this headline")
    > -----------------------------------------------------------------------------------------------------------------
    > 
    > 训练完模型之后，可以打印一下预测的结果，接下来就保存模型。
    > 
    > 保存的时候只需要一行代码 `model.save`，再给它加一个名字就可以用 `h5` 的格式保存起来。
    > 
    > 这里注意，需要已经安装了 `HDF5` 这个模块。
    > 
    > 保存完模型之后，删掉它，后面可以来比较是否成功的保存。
    > 
    > ```python
    > # save
    > print('test before save: ', model.predict(X_test[0:2]))
    > model.save('my_model.h5')   # HDF5 file, you have to pip3 install h5py if don't have it
    > del model  # deletes the existing model
    > 
    > """
    > test before save:  [[ 1.87243938] [ 2.20500779]]
    > """
    > ```
    > 
    > 导入模型并应用[](https://morvanzhou.github.io/tutorials/machine-learning/keras/3-1-save/#导入模型并应用 "Permalink to this headline")
    > -----------------------------------------------------------------------------------------------------------------------
    > 
    > 导入保存好的模型，再执行一遍预测，与之前预测的结果比较，可以发现结果是一样的。
    > 
    > ```python
    > from keras.models import load_model
    > 
    > # load
    > model = load_model('my_model.h5')
    > print('test after load: ', model.predict(X_test[0:2]))
    > 
    > """
    > test after load:  [[ 1.87243938] [ 2.20500779]]
    > """
    > ```
    > 

- [Keras 儲存與載入訓練好的模型或參數教學 - G. T. Wang](https://blog.gtwang.org/programming/keras-save-and-load-model-tutorial/)

    > Keras 儲存與載入完整模型與參數
    > ------------------
    > 
    > 我們以簡單的[手寫數字辨識 CNN 模型](https://blog.gtwang.org/programming/tensorflow-core-keras-api-cnn-tutorial/)為範例，示範如何把訓練好的模型儲存起來。在模型訓練完之後，若要儲存整個模型，只要呼叫 `save` 函數，並指定 HDF5 的檔案名稱即可：
    > 
    > ```python
    > # [略]
    > 
    > # 訓練模型
    > model.fit(x_train, y_train,
    >           batch_size=128 * 2,
    >           epochs=12,
    >           verbose=1,
    >           validation_data=(x_test, y_test))
    > 
    > # 將模型儲存至 HDF5 檔案中
    > model.save('my_model.h5')  # creates a HDF5 file 'my_model.h5'
    > ```
    > 
    > 在模型儲存至 HDF5 檔案之後，未來要使用時就可以呼叫 `keras.models.load_model` 直接載入之前訓練好的模型：
    > 
    > ```python
    > # 準備 x_test 與 y_test 資料 ... [略]
    > 
    > # 從 HDF5 檔案中載入模型
    > model = tf.contrib.keras.models.load_model('my_model.h5')
    > 
    > # 驗證模型
    > score = model.evaluate(x_test, y_test, verbose=0)
    > 
    > # 輸出結果
    > print('Test loss:', score[0])
    > print('Test accuracy:', score[1])
    > ```
    > 
    > 從 HDF5 載入的模型，使用起來跟原本的模型是一模一樣的：
    > 
    > ```
    > Test loss: 0.0300953536768
    > Test accuracy: 0.9897
    > ```
    > 
    > 只儲存與載入模型
    > --------
    > 
    > 如果只要將模型儲存起來，不儲存其中的參數，可以使用 `to_json` 或 `to_yaml` 將模型轉為 JSON 或 YAML 的文字資料，在自己儲存至檔案中：
    > 
    > ```python
    > # 將模型匯出至 JSON（不含參數）
    > json_string = model.to_json()
    > 
    > # 將模型匯出至 YAML（不含參數）
    > yaml_string = model.to_yaml()
    > ```
    > 
    > 若要從 JSON 或 YAML 重建模型，可以使用 `model_from_json` 或 `model_from_yaml`：
    > 
    > ```python
    > # 從 JSON 資料重建模型
    > model = tf.contrib.keras.models.model_from_json(json_string)
    > 
    > # 從 YAML 資料重建模型
    > model = tf.contrib.keras.models.model_from_yaml(yaml_string)
    > ```
    > 
    > 只儲存與載入參數
    > --------
    > 
    > 若只想要儲存模型的參數（也就是 weights），不包含模型本身，可以使用 `save_weights`：
    > 
    > ```python
    > # 將參數儲存至 HDF5 檔案（不含模型）
    > model.save_weights('my_model_weights.h5')
    > ```
    > 
    > 若要載入參數，可使用 `load_weights`：
    > 
    > ```python
    > # 從 HDF5 檔案載入參數（不含模型）
    > model.load_weights('my_model_weights.h5')
    > ```
    > 
    > 若要將儲存的參數載入至不同的模型中使用（模型不同，但有相同網路層，例如 fine-tuning 或 transfer-learning），可以加上 `by_name` 參數：
    > 
    > ```python
    > # 載入參數至不同的模型中使用
    > model.load_weights('my_model_weights.h5', by_name = True)
    > ```
    > 
    > ### 範例
    > 
    > 以下是一個簡單的範例，假設原始的模型如下，在原始模型訓練好之後，我們將這個模型的參數儲存下來：
    > 
    > ```python
    > # 原始模型
    > model = Sequential()
    > model.add(Dense(2, input_dim=3, name='dense_1'))
    > model.add(Dense(3, name='dense_2'))
    > 
    > # [略]
    > 
    > # 儲存參數
    > model.save_weights("weight_1.h5")
    > ```
    > 
    > 接著我們又建立另外一個新的模型，而這個新的模型與舊的模型之間有部份的網路層是相同的，在將參數載入至新模型時，只有那些相同的網路層參數會受影響，其餘的參數則不會改變：
    > 
    > ```python
    > # 新建模型
    > model = Sequential()
    > 
    > # 相同網路層，會載入參數
    > model.add(Dense(2, input_dim=3, name='dense_1'))
    > 
    > # 不同網路層，不會載入參數
    > model.add(Dense(10, name='new_dense'))
    > 
    > # 載入參數，只會影響 dense_1 那一層
    > model.load_weights(fname, by_name = True
    > ```
    > 
    > 自訂類別
    > ----
    > 
    > 若在模型中有包含自訂的網路層、類別或函數等，可在載入時加入 `custom_objects` 自訂物件參數，使其正常載入：
    > 
    > ```python
    > # 假設模型中有包含一個自訂的 AttentionLayer 類別實體
    > model = tf.contrib.keras.models.load_model('my_model.h5',
    >   custom_objects = {'AttentionLayer': AttentionLayer})
    > ```
    > 
    > 亦可使用 `CustomObjectScope` 來載入自訂的類別實體：
    > 
    > ```python
    > # 亦可使用 custom object scope 來載入自訂的類別實體
    > with CustomObjectScope({'AttentionLayer': AttentionLayer}):
    >   model = load_model('my_model.h5')
    >  ```
    > 
    > 自訂物件參數的用法，在 `load_model`、`model_from_json` 與 `model_from_yaml` 中都相同：
    > 
    > ```python
    > # 從 JSON 資料中載入
    > model = model_from_json(json_string, custom_objects={'AttentionLayer': AttentionLayer})
    > ```
    > 
    > 常見問題
    > ----
    > 
    > 若在儲存或載入 HDF5 檔案時出現這樣的錯誤：
    > ```
    > ImportError: `save_model` requires h5py.
    > ```
    > 代表系統上少裝了 `h5py`，用 `pip` 裝一下即可：
    > ```
    > pip install h5py
    > ```
    > 


## Troubleshooting

- [ImportError: No module named h5py · Issue #3426 · keras-team/keras](https://github.com/keras-team/keras/issues/3426)

    > On windows 10, I executed
    > 
    > ```
    > pip install h5py
    > pip install cython
    > ```
    > 
    > 
    > UPDATE: ok....so I uninstalled h5py and then reinstalled it and restarted anaconda. Now its working!!!

- [Loading model with custom loss function: ValueError: 'Unknown loss function' · Issue #5916 · keras-team/keras](https://github.com/keras-team/keras/issues/5916)
    
    > I solved this problem by adding 'custom_bojects'
    > 
    > ```
    > model = load_model('model/multi_task/try.h5', custom_objects={'loss_max': loss_max})
    > ```
    > 
    > my loss function:
    > 
    > ```
    > def loss_max(y_true, y_pred):
    >     from keras import backend as K
    >     return K.max(K.abs(y_pred - y_true), axis=-1)
    > ```
    > 