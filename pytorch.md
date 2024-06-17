[toc]



# pytorch

### 常用命令

#### 创建张量方式 :m:（data：根据矩阵数据创建；shape：根据形状创建）

- torch.tensor(data) 
- torch.Tensor(shape/data) 
- torch.IntTensor()、FloatTensor()、DoubleTensor()
- torch.randn(shape): 创建随机张量（正态）
- torch.ones(shape)、torch.ones_like(data)：全1张量
- torch.zeros(shape)、torch.zeros_like(data)：全0张量
- torch.full(shape, n)、torch.full_like(data, n)：全n张量

#### 创建线性和随机张量(step：步长；length：长度 )

torch.arrange(start, end, step) 和 torch.linspace(start, end, length)

#### 设置随机种子

torch.random.initial_seed() 和 torch.random.manual_seed()

#### 类型转换

- data.type(torch.DoubleTensor)
- data.double()、data.int()....

#### 基本运算（带下划线的会修改原值）

- add/add_：加法
- sub/sub_：减法
- mul / mul_ / *：乘法（点乘）
- matmul / @ : 矩阵乘法
- div/div_：除法
- neg/neg_：取负数

#### 基本函数

- data.mean(dim)
- data.sum(dim)
- torch.pow(data, n) : 幂函数
- data.sqrt()：平方根
- data.exp(n) ：指数 $e^n$ 
- data.log() ：对数，底数为e。（ log2(), log10() ）

#### numpy 与 torch

- 两种类型相互转化：  

```python 
# 该时候是共享内存的（浅拷贝）
data_tensor = torch.from_numpy(data_numpy) 
# 深拷贝转换
data_tensor = torch.tensor(data_numpy)
data_tensor = torch.from_numpy(data_numpy).copy()
```

#### 列表索引

```python
'''
假设data为2维张量
'''
# 返回（0， 1）、 （1， 2）两个位置的元素
data[[0, 1], [1, 2]]
# 返回（0， 1）行 （1， 2）列四个位置的元素
data[[[0], [1]], [1, 2]]

# 前3行前2列数据
data[:3, :2]

'''
布尔索引
'''
# 第3列大于5的行数据
data[data[:, 2] > 5]
# 第2行大于5的列数据
data[:, data[1] > 5]
```

#### 形状操作

1. data.reshape(shape)

2. data.squeeze(dim)：在dim上降维

3. data.unsqueeze(dim)：在dim上升维

4. torch.transpose(data, m, n) ：交换维度m, 维度n

5. torch.permute(data, shape)：把形状变为shape

6. data.view(a1, a2, a3, ...)：
   把data转换为shape为$[a1, a2, a3, ...]$ 的张量
   ==但是view转换的张量只能位于连续内存中, 如果一个数据经过transpose或者permute处理后，就无法使用view函数进行操作。== 

   ```python
   # 判断data是否在连续内存中
   data.is_contiguous() # True or False
   ```

7. data.contiguous()
   ==转换为连续内存的数据，一般配合view使用==

#### 张量拼接

- torch.cat([data1, data2], dim)
  data1 和 data2 在维度dim上拼接。