---
layout: post
title:  "Issues on torch MSE feature-wise mean calculations"
categories: pytorch
---

From torch documents, 

`torch.nn.MSELoss` calls `F.MSE_loss` then calls `C api`

and by default it's said to be an *element_wise* error, i.e. 

$$ input\_loss = \Sigma_{i=1} ^{N} (Y_i - Y)**2 / (N * \#feat) $$



Yet this left one problem to be confirmed:

when the `reduction` param set to `sum` instead of the default `mean`, the behavior of the operator I suppose to be:

$$ input\_loss = \Sigma_{i=1} ^{N} (Y_i - Y)**2 / \#feat $$

i.e. it shall downgrade to feature-wise mean square error.

But in practice, I found that with a input size of 192 the input-loss is at a level of 300-400, and with a size of 10, it reduces to 10-0.1. That said, the input loss cannot be directly compared.



**Question** left to reason about such **a big gap** in the above two sizes, whether it's caused by **UNDERFITTING** due to a much large network of dimension 192 compared to dimension 10.



Will come back later to fill the answer when experiments conducted in the future.

