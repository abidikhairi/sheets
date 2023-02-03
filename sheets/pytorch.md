# PyTorch

### add empty dimension to tensor

```python
x = torch.randn(10, 15)

print(x.shape)
# prints: (10, 15)

y1 = x.unsqueeze(dim=0)
y2 = x.unsqueeze(dim=2)

print(y1.shape)
# prints: (1, 10, 15)

print(y2.shape)
# prints: (10, 15, 1)
```

### remove empty dimension

```python
x = torch.randn(10, 15, 1)

y = x.squeeze(dim=2)

print(y.shape)
# prints: (10, 15)
```

### masked fill
```python
mask = th.randint(0, 2, (1, 5))
x = th.randn(1, 5)
y = x.masked_fill(mask, 0.0)

print(x)
# prints: tensor([[-0.6791,  0.5190, -0.4090, -0.5270, -0.3954]])
print(mask)
# prints: tensor([[0, 1, 0, 0, 0]])
print(y)
# prints: tensor([[-0.6791,  0.0000, -0.4090, -0.5270, -0.3954]])
```
