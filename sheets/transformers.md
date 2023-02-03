# Transformers

### Self Attention Layer

```python
import torch as th

def scaled_dot_product(q, k, v):
    socres = th.bmm(q, k.permute(1, 2))

    scores = th.softmax(scores / q.size(2), dim=-1)

    return th.bmm(scores, v.permute(1, 2))

x = th.randn(8, 20, 128)
# (batch_size, seq_len, d_model)

h = scaled_dot_product(x, x, x)
# (batch_size, seq_len, d_model)
```