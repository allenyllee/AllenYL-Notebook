# Keras__深度學習

[toc]
<!-- toc --> 

## API reference

- [Sequential - Keras Documentation](https://keras.io/models/sequential/)

- keras.layers
    - [Core Layers - Keras Documentation](https://keras.io/layers/core/)
    
        > ### Dense
        > 
        > ```
        > keras.layers.Dense(units, activation=None, use_bias=True, kernel_initializer='glorot_uniform', bias_initializer='zeros', kernel_regularizer=None, bias_regularizer=None, activity_regularizer=None, kernel_constraint=None, bias_constraint=None)
        > ```
        > 
        > Just your regular densely-connected NN layer.


        > ### Dropout
        > 
        > ```
        > keras.layers.Dropout(rate, noise_shape=None, seed=None)
        > 
        > ```
        > 
        > Applies Dropout to the input.


        > ### Flatten
        > 
        > ```
        > keras.layers.Flatten()
        > 
        > ```
        > 
        > Flattens the input. Does not affect the batch size.

        __example__
        > flat = Flatten()(conv4)
        > 
        > dense1 = Dense(units=256, activation='relu' )(flat)
        > dense1 = Dropout(0.5)(dense1)
        > 
        > dense1 = Dense(units=256, activation='relu')(dense1)
        > dense1 = Dropout(0.5)(dense1)
        > 
        > dense3 = Dense(y_train.shape[1], activation='softmax')(dense1)
        > 
        > model = Model(inputs=inputs, outputs=dense3)





- [Losses - Keras Documentation](https://keras.io/losses/#available-loss-functions)

- [Initializers - Keras Documentation](https://keras.io/initializers/)

- [Optimizers - Keras Documentation](https://keras.io/optimizers/)

- [Metrics - Keras Documentation](https://faroit.github.io/keras-docs/1.1.1/metrics/)

### split train & test data

- [Split train data into training and validation when using ImageDataGenerator and model.fit_generator · Issue #5862 · keras-team/keras](https://github.com/keras-team/keras/issues/5862)

    > It's very simple, split your data set indices when they are read e.g., with glob  
    > train\_samples, validation\_samples = train\_test\_split(Image\_List, test\_size=0.2)  
    > and then feed train sample to train generator and test sample to validation generator.

### Model functional API

- [Model (functional API) - Keras Documentation](https://keras.io/models/model/)

    > In the functional API, given some input tensor(s) and output tensor(s), you can instantiate a `Model` via:
    > 
    > ```
    > from keras.models import Model
    > from keras.layers import Input, Dense
    > 
    > a = Input(shape=(32,))
    > b = Dense(32)(a)
    > model = Model(inputs=a, outputs=b)
    > ```
    > 
    > This model will include all layers required in the computation of `b` given `a`.
    > 
    > In the case of multi-input or multi-output models, you can use lists as well:
    > 
    > ```
    > model = Model(inputs=[a1, a2], outputs=[b1, b2, b3])
    > ```




### ImageDataGenerator

- [Image Preprocessing - Keras Documentation](https://keras.io/preprocessing/image/)

    > ```
    > keras.preprocessing.image.ImageDataGenerator(featurewise_center=False, samplewise_center=False, featurewise_std_normalization=False, samplewise_std_normalization=False, zca_whitening=False, zca_epsilon=1e-06, rotation_range=0.0, width_shift_range=0.0, height_shift_range=0.0, brightness_range=None, shear_range=0.0, zoom_range=0.0, channel_shift_range=0.0, fill_mode='nearest', cval=0.0, horizontal_flip=False, vertical_flip=False, rescale=None, preprocessing_function=None, data_format=None, validation_split=0.0)
    > ```
    > 
    > Generate batches of tensor image data with real-time data augmentation. The data will be looped over (in batches).


    > **Examples**
    > 
    > Example of using `.flow(x, y)`:
    > 
    > ```
    > (x_train, y_train), (x_test, y_test) = cifar10.load_data()
    > y_train = np_utils.to_categorical(y_train, num_classes)
    > y_test = np_utils.to_categorical(y_test, num_classes)
    > 
    > datagen = ImageDataGenerator(
    >     featurewise_center=True,
    >     featurewise_std_normalization=True,
    >     rotation_range=20,
    >     width_shift_range=0.2,
    >     height_shift_range=0.2,
    >     horizontal_flip=True)
    > 
    > # compute quantities required for featurewise normalization
    > # (std, mean, and principal components if ZCA whitening is applied)
    > datagen.fit(x_train)
    > 
    > # fits the model on batches with real-time data augmentation:
    > model.fit_generator(datagen.flow(x_train, y_train, batch_size=32),
    >                     steps_per_epoch=len(x_train) / 32, epochs=epochs)
    > 
    > # here's a more "manual" example
    > for e in range(epochs):
    >     print('Epoch', e)
    >     batches = 0
    >     for x_batch, y_batch in datagen.flow(x_train, y_train, batch_size=32):
    >         model.fit(x_batch, y_batch)
    >         batches += 1
    >         if batches >= len(x_train) / 32:
    >             # we need to break the loop by hand because
    >             # the generator loops indefinitely
    >             break
    > 
    > ```

    > Example of using `.flow_from_directory(directory)`:
    > 
    > ```
    > train_datagen = ImageDataGenerator(
    >         rescale=1./255,
    >         shear_range=0.2,
    >         zoom_range=0.2,
    >         horizontal_flip=True)
    > 
    > test_datagen = ImageDataGenerator(rescale=1./255)
    > 
    > train_generator = train_datagen.flow_from_directory(
    >         'data/train',
    >         target_size=(150, 150),
    >         batch_size=32,
    >         class_mode='binary')
    > 
    > validation_generator = test_datagen.flow_from_directory(
    >         'data/validation',
    >         target_size=(150, 150),
    >         batch_size=32,
    >         class_mode='binary')
    > 
    > model.fit_generator(
    >         train_generator,
    >         steps_per_epoch=2000,
    >         epochs=50,
    >         validation_data=validation_generator,
    >         validation_steps=800)
    > 
    > ```
    > 


- [Split train data into training and validation when using ImageDataGenerator and model.fit_generator · Issue #5862 · keras-team/keras](https://github.com/keras-team/keras/issues/5862#issuecomment-397976696)

    > I just found this in the documentation given [here](https://keras.io/preprocessing/image/).
    > 
    > You have to specify `validation_split` in the `ImageDataGenerator` and specify `subset` for each generator as shown below:
    > 
    > ```
    > from keras.preprocessing.image import ImageDataGenerator
    > 
    > data_generator = ImageDataGenerator(rescale=1./255, validation_split=0.33)
    > 
    > train_generator = data_generator.flow_from_directory(TRAINING_DIR, target_size=(IMAGE_SIZE, IMAGE_SIZE), shuffle=True, seed=13,
    >                                                      class_mode='categorical', batch_size=BATCH_SIZE, subset="training")
    > 
    > validation_generator = data_generator.flow_from_directory(TRAINING_DIR, target_size=(IMAGE_SIZE, IMAGE_SIZE), shuffle=True, seed=13,
    >                                                      class_mode='categorical', batch_size=BATCH_SIZE, subset="validation")
    > 
    > ```




### Callbacks

- [Callbacks - Keras Documentation](https://keras.io/callbacks/#earlystopping)

    > ### EarlyStopping
    > 
    > ```
    > keras.callbacks.EarlyStopping(monitor='val_loss', min_delta=0, patience=0, verbose=0, mode='auto')
    > ```
    > 
    > Stop training when a monitored quantity has stopped improving.
    > 


    > ### ModelCheckpoint
    > 
    > ```python
    > keras.callbacks.ModelCheckpoint(filepath, monitor='val_loss', verbose=0, save_best_only=False, save_weights_only=False, mode='auto', period=1)
    > ```
    > 
    > Save the model after every epoch.

    > ### Example: model checkpoints
    > 
    > ```python
    > from keras.callbacks import ModelCheckpoint
    > 
    > model = Sequential()
    > model.add(Dense(10, input_dim=784, kernel_initializer='uniform'))
    > model.add(Activation('softmax'))
    > model.compile(loss='categorical_crossentropy', optimizer='rmsprop')
    > 
    > '''
    > saves the model weights after each epoch if the validation loss decreased
    > '''
    > checkpointer = ModelCheckpoint(filepath='/tmp/weights.hdf5', verbose=1, save_best_only=True)
    > model.fit(x_train, y_train, batch_size=128, epochs=20, verbose=0, validation_data=(X_test, Y_test), callbacks=[checkpointer])
    >```



### pre-trained model

- [pre-trained model Applications - Keras Documentation](https://keras.io/applications/)

    > Documentation for individual models
    > ===================================
    > 
    > | Model | Size | Top-1 Accuracy | Top-5 Accuracy | Parameters | Depth |
    > | --- | --: | --: | --: | --: | --: |
    > | [Xception](https://keras.io/applications/#xception) | 88 MB | 0.790 | 0.945 | 22,910,480 | 126 |
    > | [VGG16](https://keras.io/applications/#vgg16) | 528 MB | 0.715 | 0.901 | 138,357,544 | 23 |
    > | [VGG19](https://keras.io/applications/#vgg19) | 549 MB | 0.727 | 0.910 | 143,667,240 | 26 |
    > | [ResNet50](https://keras.io/applications/#resnet50) | 99 MB | 0.759 | 0.929 | 25,636,712 | 168 |
    > | [InceptionV3](https://keras.io/applications/#inceptionv3) | 92 MB | 0.788 | 0.944 | 23,851,784 | 159 |
    > | [InceptionResNetV2](https://keras.io/applications/#inceptionresnetv2) | 215 MB | 0.804 | 0.953 | 55,873,736 | 572 |
    > | [MobileNet](https://keras.io/applications/#mobilenet) | 17 MB | 0.665 | 0.871 | 4,253,864 | 88 |
    > | [DenseNet121](https://keras.io/applications/#densenet) | 33 MB | 0.745 | 0.918 | 8,062,504 | 121 |
    > | [DenseNet169](https://keras.io/applications/#densenet) | 57 MB | 0.759 | 0.928 | 14,307,880 | 169 |
    > | [DenseNet201](https://keras.io/applications/#densenet) | 80 MB | 0.770 | 0.933 | 20,242,984 | 201 |
    > 

## Tutorial

- [Guide to the Sequential model - Keras Documentation](https://keras.io/getting-started/sequential-model-guide/#compilation)

- [陳雲濤的部落格: Keras 學習筆記](https://violin-tao.blogspot.tw/2017/05/keras.html)

### RNN

#### 用RNN 預測 sin波型
- [RNN Regressor 循环神经网络 - Keras | 莫烦Python](https://morvanzhou.github.io/tutorials/machine-learning/keras/2-5-RNN-LSTM-Regressor/)

- [tensorflow - predict sinus with keras feed forward neural network - Data Science Stack Exchange](https://datascience.stackexchange.com/questions/19365/predict-sinus-with-keras-feed-forward-neural-network)

    > Accuracy is a metric meant for classification problems, look at the mean squared error instead. Your network is too small for a highly fluctuating function that you want to learn, if you divide your x by a smaller amount it would be easier to learn. Second of all, adding another layer and having an identity activation at the end will help quite a bit. Also taking batches bigger than 1 will make the gradient more stable. With a 1000 epochs I get to 0.00167 as mean squared error.
    > 
    > ```
    > x = np.arange(200).reshape(-1,1) / 50
    > y = np.sin(x)
    > 
    > model = Sequential([
    > Dense(40, input_shape=(1,)),
    > Activation('sigmoid'),
    > Dense(12),
    > Activation('sigmoid'),
    > Dense(1)
    >     ])
    > 
    > model.compile(loss='mean_squared_error', optimizer='SGD', metrics=['mean_squared_error'])
    > 
    > for i in range(40):
    >     model.fit(x, y, nb_epoch=25, batch_size=8, verbose=0)
    >     predictions = model.predict(x)
    >     print(np.mean(np.square(predictions - y)))
    > 
    > ```
    > 
    > The biggest issue is that the signal in your original small dataset is very difficult to learn, you can see this when you plot it, it will just collapse to the mean.

    > Keep in mind that the **Accuracy** measure is measuring whether the values are _Exactly The Same_. I.e. it is a classification measure, whereas approximating a sin curve is much better suited for measurement as a regression problem.
    > 
    > That said:
    > 
    > In evaluating the network's performance, what is the network actually doing? Let's take the network and perform a little visual analysis on its performance:
    > 
    > ```
    > import matplotlib.pyplot as plt
    > preds = model.predict(x)
    > plt.plot(x, y, 'b', x, preds, 'r--')
    > plt.ylabel('Y / Predicted Value')
    > plt.xlabel('X Value')
    > plt.show()
    > 
    > ```
    > 
    > [![enter image description here](https://i.stack.imgur.com/e0acv.png)](https://i.stack.imgur.com/e0acv.png)
    > 
    > Hmm. The model seems to be minimizing error by simply getting closer and closer to guessing 0 for every value, rather than approximating the function. There are several hypotheses here to explain this. One is that the network is not complex enough to model the function. In order to test this, let's simplify the function- that is, let's bring the range down to one sine cycle:
    > 
    > ```
    > x = np.arange(0, math.pi*2, 0.1)
    > y = np.sin(x)
    > 
    > ```
    > 
    > And try to train the network again:
    > 
    > [![enter image description here](https://i.stack.imgur.com/8HA7X.png)](https://i.stack.imgur.com/8HA7X.png)
    > 
    > Not wonderful, but a better fit, certainly.
    > 
    > How about with **100 epochs** instead of 10?
    > 
    > [![enter image description here](https://i.stack.imgur.com/0Q6eS.png)](https://i.stack.imgur.com/0Q6eS.png)
    > 
    > How about with **1000 epochs**?
    > 
    > [![enter image description here](https://i.stack.imgur.com/Wk7qL.png)](https://i.stack.imgur.com/Wk7qL.png)
    > 
    > This is, of course, very interesting. After 1000 epochs, our networks is able to roughly approximate the downward curve from 1:0 (π /2  
    > 
    > : π   ) of the sine response, but not the initial upward curve 0:1 (0:π /2  ) or the region in which the function is negative (π   :2π   
    > 
    > ).
    > 
    > This result begs the question- what will it look like after **10000 epochs**?
    > 
    > [![enter image description here](https://i.stack.imgur.com/sxf00.png)](https://i.stack.imgur.com/sxf00.png)
    > 
    > Not significantly better. It looks like we'll have to change the architecture of the network (more layers, more neurons, and/or different activation functions) to improve beyond this point.
    > 
    > To inform this architecture change, let's take a look at the sigmoid activation function:
    > 
    > [![enter image description here](https://i.stack.imgur.com/pp6kl.png)](https://i.stack.imgur.com/pp6kl.png)
    > 
    > Uh-oh. The value of this sigmoid function can only ever be in the range 0:1, and the range of the sin function is -1:1.
    > 
    > To correct this, let's just normalize the sin response between 0 and 1:
    > 
    > ```
    > y = (np.sin(x)+1)/2 
    > 
    > ```
    > 
    > Now, the network performs much better than before after 1000 epochs:
    > 
    > [![enter image description here](https://i.stack.imgur.com/X0Nrk.png)](https://i.stack.imgur.com/X0Nrk.png)
    > 
    > And 10000:
    > 
    > [![enter image description here](https://i.stack.imgur.com/IxcxR.png)](https://i.stack.imgur.com/IxcxR.png)
    > 
    > After 100000 epochs, it's roughly perfect:
    > 
    > [![enter image description here](https://i.stack.imgur.com/dmbZb.png)](https://i.stack.imgur.com/dmbZb.png)
    > 
    > Even still, this advancement doesn't help much on the larger sin range (after 1000 epochs):
    > 
    > ```
    > x = np.arange(0, 100, 1)
    > y = (np.sin(x)+1)/2 
    > 
    > ```
    > 
    > [![enter image description here](https://i.stack.imgur.com/6smI5.png)](https://i.stack.imgur.com/6smI5.png)
    > 
    > If we, however, take the model trained on a single sin curve and further train it on the larger range, we begin to see progress after 1000 epochs:
    > 
    > ```
    > x = np.arange(0, 100, .1)
    > y = (np.sin(x)+1)/2 
    > 
    > model_copy = model
    > model_copy.fit(x, y, epochs=1000, batch_size=8, verbose=0)
    > model_copy_preds = model_copy.predict(x)
    > 
    > ```
    > 
    > [![enter image description here](https://i.stack.imgur.com/UW8H2.png)](https://i.stack.imgur.com/UW8H2.png)
    > 
    > And more so after 10000 epochs:[![enter image description here](https://i.stack.imgur.com/cmQjw.png)](https://i.stack.imgur.com/cmQjw.png)
    > 
    > And more so, well into the third repetition after 100000 epochs:
    > 
    > [![enter image description here](https://i.stack.imgur.com/zDPgJ.png)](https://i.stack.imgur.com/zDPgJ.png)
    > 
    > So, with careful training, our network with a single layer of sigmoid activations appears to be learning to generalize the sin curve. Further investigation could find a limit to that generalization, certainly.
    > 
    > For reproduction:
    > 
    > ```
    > import numpy as np
    > from keras.layers import Dense
    > from keras.models import Sequential
    > import matplotlib.pyplot as plt
    > import math
    > 
    > x = np.arange(0, math.pi*2, .1)
    > y = (np.sin(x)+1)/2 
    > 
    > model = Sequential([
    >     Dense(10, input_shape=(1,)),
    >     Activation('sigmoid'),
    >     Dense(1)
    > ])
    > 
    > model.compile(loss='mean_squared_error', optimizer='SGD', metrics=['mean_squared_error'])
    > model.fit(x, y, epochs=100000, batch_size=8, verbose=0)
    > 
    > preds = model.predict(x)
    > 
    > plt.plot(x, y, 'b', x, preds, 'r--')
    > plt.ylabel('Y / Predicted Value')
    > plt.xlabel('X Value')
    > plt.show()
    > 
    > x = np.arange(0, 100, .1)
    > y = (np.sin(x)+1)/2 
    > 
    > model_copy = model
    > model_copy.fit(x, y, epochs=10000, batch_size=8, verbose=0)
    > model_copy_preds = model_copy.predict(x)
    > 
    > plt.plot(x, y, 'b', x, model_copy_preds, 'r--')
    > plt.ylabel('Y / Predicted Value')
    > plt.xlabel('X Value')
    > plt.show()
    > 
    > ```
    > 

- [python - Approximating sine function with Neural Network and ReLU (Keras) - Stack Overflow](https://stackoverflow.com/questions/44716415/approximating-sine-function-with-neural-network-and-relu-keras)

    > Two things here:
    > 
    > 1.  Your network is really shallow and small. Having only 4 neurons with `relu` makes a case when a couple of this neurons are completely saturated highly possible. This is probably why your network result looks like that. Try `he_normal` or `he_uniform` as initializer to overcome that.
    > 2.  In my opinion your network is too small for this task. I would definitely increase both depth and width of your network by intdoucing more neurons and layers to your network. In case of `sigmoid` which has a similiar shape to a `sin` function this might work fine - but in case of `relu` you really need a bigger network.



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

### GPU Usage

- [python - Can I run Keras model on gpu? - Stack Overflow](https://stackoverflow.com/questions/45662253/can-i-run-keras-model-on-gpu)

    > Yes you can run keras models on GPU. Few things you will have to check first.
    > 
    > 1.  your system has GPU (Nvidia. As AMD doesn't work yet)
    > 2.  You have installed the GPU version of tensorflow
    > 3.  You have installed CUDA [installation instructions](https://www.tensorflow.org/install/install_linux)
    > 4.  Verify that tensorflow is running with GPU [check if GPU is working](https://stackoverflow.com/questions/38009682/how-to-tell-if-tensorflow-is-using-gpu-acceleration-from-inside-python-shell)
    > 
    > `sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))`
    > 
    > OR
    > 
    > `from tensorflow.python.client import device_lib`
    > 
    > `print(device_lib.list_local_devices())`
    > 
    > output will be something like this:
    > 
    > ```
    > [
    >   name: "/cpu:0"device_type: "CPU",
    >   name: "/gpu:0"device_type: "GPU"
    > ]
    > ```
    > 
    > Once all this is done your model will run on GPU:
    > 
    > To Check if keras(>=2.1.1) is using GPU:
    > 
    > ```
    > from keras import backend as K
    > K.tensorflow_backend._get_available_gpus()
    > ```
    > 
    > All the best.

