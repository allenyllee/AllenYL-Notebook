# 機器學習框架1-1_Pytorch

[toc]
<!-- toc --> 

# torch API

## torch.max()

- [torch — PyTorch master documentation](https://pytorch.org/docs/stable/torch.html#torch.max)


# torchvision API
## torchvision.transforms.compose()

- [torchvision.transforms — PyTorch master documentation](https://pytorch.org/docs/stable/torchvision/transforms.html#torchvision.transforms.Compose)

# torch.autograd API

## Variable (deprecated)

- [Automatic differentiation package - torch.autograd — PyTorch master documentation](https://pytorch.org/docs/stable/autograd.html#variable-deprecated)




# Pytorch vs. Tensorflow

- [用PyTorch还是TensorFlow？斯坦福大学CS博士生带来全面解答 | 雷锋网](https://www.leiphone.com/news/201708/Npflmddi8OGbnJHi.html)

- [The Star Also Rises: PyTorch（二）：PyTorch vs. TensorFlow](https://hemingwang.blogspot.tw/2017/11/pytorchpytorch-vs-tensorflow.html)

    > 結論：
    > 
    > 假定你是學生的話，可以先用 PyTorch 熟悉深度學習。但在畢業準備上班前，就要下點功夫在 TensorFlow 上，未來才方便找工作。
    > 
    > 總之，入門還是以 PyTorch 好 [7]！


# Machine Learning Implement in Pytorch

## Basic VAE Example

- [examples/vae at master · pytorch/examples](https://github.com/pytorch/examples/tree/master/vae)





# Trobuleshooting

## Loss.backward() raises error 'grad can be implicitly created only for scalar outputs'

- [Loss.backward() raises error 'grad can be implicitly created only for scalar outputs' - autograd - PyTorch Forums](https://discuss.pytorch.org/t/loss-backward-raises-error-grad-can-be-implicitly-created-only-for-scalar-outputs/12152)

    > Hi,
    > 
    > `loss.backward()` do not go through while training and throws an error when on multiple GPUs using torch.nn.DataParallel
    > 
    > `grad can be implicitly created only for scalar outputs`
    > 
    > But, the same thing trains fine when I give only `deviced_ids=[0]` to torch.nn.DataParallel.\
    > Is there something I am missing here?
    > 
    > Addendum:
    > 
    > While running on two gpus, the loss function returns a vector of 2 loss values. If I run the backward only on the first element of the vector it goes fine.
    > 
    > How can I make the backward function work with vector containing two or more loss values?
    > 
    > Thanks.
    > 
    > ---
    > 
    > when you do `loss.backward()`, it is a shortcut for `loss.backward(torch.Tensor([1]))`. This in only valid if `loss` is a tensor containing a single element.
    > 
    > `DataParallel` returns to you the partial loss that was computed on each gpu, so you usually want to do `loss.backward(torch.Tensor([1, 1]))` or `loss.sum().backward()`. Both will have the exact same behaviour.



