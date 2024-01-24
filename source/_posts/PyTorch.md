---
title: PyTorch
date: 2024-01-24 18:37:30
tags:
 - PyTorch
 - Note
category: Python
mathjax: true
---

# 关于PyTorch的使用记录

## 介绍

PyTorch 是一个开源的机器学习框架，它提供了一个灵活的深度学习平台，广泛用于各种机器学习和深度学习任务。

```python
import torch
```


## 基本用法

**张量（Tensors）**：PyTorch 的核心数据结构是张量，类似于 NumPy 的多维数组，但能够在 GPU 上运行，加速深度学习模型的训练。你可以使用 `torch.Tensor` 类来创建张量。

```python
import torch

# 创建一个张量
x = torch.Tensor([1, 2, 3])
```

---

**自动微分（Autograd）**：PyTorch 提供了自动微分功能，允许你轻松地计算梯度并进行反向传播，这对于训练神经网络非常重要。

```python
import torch

# 创建需要计算梯度的张量
x = torch.tensor(2.0, requires_grad=True)

# 定义一个计算图
y = x**2 + 3*x + 1

# 计算梯度
y.backward()

# 打印梯度
print(x.grad)  # 输出 7.0
```

---

**神经网络（Neural Networks）**：PyTorch 提供了一个模块化的神经网络库，允许你构建和训练各种深度学习模型。`torch.nn` 模块包含了构建神经网络所需的各种层和损失函数。

```python
import torch
import torch.nn as nn

# 定义一个简单的神经网络模型
class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        self.fc1 = nn.Linear(2, 3)
        self.fc2 = nn.Linear(3, 1)
        
    def forward(self, x):
        x = torch.relu(self.fc1(x))
        x = self.fc2(x)
        return x

# 创建模型实例
model = Net()
```

---

**数据加载和处理**：PyTorch 提供了 `torch.utils.data` 模块，用于创建数据集和数据加载器，方便加载和预处理训练数据。

```python
from torch.utils.data import Dataset, DataLoader

# 自定义数据集类
class CustomDataset(Dataset):
    def __init__(self, data, labels):
        self.data = data
        self.labels = labels
    
    def __len__(self):
        return len(self.data)
    
    def __getitem__(self, idx):
        return self.data[idx], self.labels[idx]

# 创建数据集和数据加载器
dataset = CustomDataset(data, labels)
dataloader = DataLoader(dataset, batch_size=32, shuffle=True)
```

---

**优化器（Optimizers）**：PyTorch 提供了各种优化器，如 SGD、Adam、RMSprop 等，用于训练神经网络。

```python
import torch.optim as optim

# 定义优化器
optimizer = optim.Adam(model.parameters(), lr=0.001)

# 在训练循环中使用优化器
optimizer.zero_grad()
outputs = model(inputs)
loss = criterion(outputs, targets)
loss.backward()
optimizer.step()
```

---

**GPU 支持**：PyTorch 支持在 GPU 上训练模型，以加速深度学习任务。你可以使用 `.to(device)` 来将张量和模型移动到 GPU。

```python
import torch

# 检查 GPU 是否可用
device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")

# 将张量和模型移动到 GPU
x = x.to(device)
model = model.to(device)
```

---

**保存和加载模型**：你可以使用 `torch.save` 和 `torch.load` 来保存和加载 PyTorch 模型。

```python
import torch

# 保存模型
torch.save(model.state_dict(), 'model.pth')

# 加载模型
model.load_state_dict(torch.load('model.pth'))
model.eval()  # 设置模型为评估模式
```

---

未完待续

