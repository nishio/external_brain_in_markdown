
- Torch
    - [http://torch.ch/docs/getting-started.html](http://torch.ch/docs/getting-started.html)
    - これをインストールしてしまったがこれではなくPyTorchを入れる必要があった

- `$ pip3 install torch`
- > Successfully installed torch-0.4.1


:

```
x.index_fill_?
Docstring:
index_fill_(dim, index, val) -> Tensor

Fills the elements of the :attr:`self` tensor with value :attr:`val` by
selecting the indices in the order given in :attr:`index`.

Args:
    dim (int): dimension along which to index
    index (LongTensor): indices of :attr:`self` tensor to fill in
    val (float): the value to fill with

Example::
    >>> x = torch.tensor([[1, 2, 3], [4, 5, 6], [7, 8, 9]], dtype=torch.float)
    >>> index = torch.tensor([0, 2])
    >>> x.index_fill_(1, index, -1)
    tensor([[-1.,  2., -1.],
            [-1.,  5., -1.],
            [-1.,  8., -1.]])
Type:      builtin_function_or_method
```

indexが空のTensorである場合にエラー

> Expected object of type torch.FloatTensor but found type torch.LongTensor


:

```
scatter_(dim, index, src) -> Tensor

Args:
    dim (int): the axis along which to index
    index (LongTensor): the indices of elements to scatter
    src (Tensor or float): the source element(s) to scatter
```


