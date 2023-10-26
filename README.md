# DiveIntoCHAIRSKingdom
Give you a rough yet clear explanation about the CHAIRS dataset.
DICK, Dive Into CHAIRS Kingdom

### 以下数据来自Koyui evaluation

选取物体为第64个，对应序列的文件夹为0289，0290，0291，0292，0293，0294，0295，0296，0297，0301，0302，0303，0304，0305和0306

比较好的一个遍历序列写法为

```python
seqs = list(range(289, 298)) + list(range(301, 307))
seqs = list(map(lambda x: '0' + str(x), seqs))
```

在跑数据集的时候，主要遇到了两种情况：

- 在图片文件夹下的某张图片并不对应具体的一百多万帧下的任何一帧，因此没有关于该图片的任何数据，被我定义为 **Invalid Frame**（该文件夹中顺序数第几张图片，从0开始）
- Phosa在跑这张图片的时候人物捕捉失败，所以其他数据集在评估的时候也不应跑动，被我定义为 **Phosa Not Run**（该文件夹中顺序数第几张图片，从0开始）

对应的处理办法为下：

|   序列   | 能跑的帧数/总帧数 | Invalid Frame |           Phosa Not Run           |
| :------: | :---------------: | :-----------: | :-------------------------------: |
|   0289   |      242/243      |               |                68                 |
|   0290   |      193/201      |      200      | 160，161，165，166，167，171，172 |
|   0291   |      234/235      |               |                48                 |
|   0292   |      331/331      |               |                                   |
|   0293   |      202/202      |               |                                   |
|   0294   |      272/273      |               |                83                 |
|   0295   |      238/238      |               |                                   |
|   0296   |      245/246      |      245      |                                   |
|   0297   |      240/241      |      240      |                                   |
|   0301   |      267/268      |      267      |                                   |
|   0302   |      276/277      |      276      |                                   |
|   0303   |      271/271      |               |                                   |
|   0304   |      275/276      |      275      |                                   |
|   0305   |      301/302      |      301      |                                   |
|   0306   |      264/264      |               |                                   |
| **总计** |     3851/3868     |       7       |                10                 |

对应的字典请参照notRun.py

### 我该如何找到图片对应的某帧，以及如何找到图片对应的GT？

首先，对于你跑的某一文件夹下的某个图片，例如0289下0视角（只有0视角）的第6张图片**（从0开始编号所以索引为5）**

```cmd
AI-being:\zhaochf\experiments\PHOSA\CHAIRS\0289\0\5\frame.txt
```

会告诉你，这张图片对应CHAIRS的123541帧。

公式（要改的地方）：

```cmd
AI-being:\zhaochf\experiments\PHOSA\CHAIRS\{第几个序列}\0\{第几张图片，0开始标号}\frame.txt
```

接下来，如果你想寻找ground truth，只需要访问

```cmd
share_folder:\ho_datasets\CHAIRS\human_GT\64\123541
```

以及

```cmd
share_folder:\ho_datasets\CHAIRS\object_GT\64\123541
```

最后一个帧数改一下就可以了。

humanGT目录下data.json是smpl数据，请忽略joints.txt/joints.json，但人的第一关节点的位移对于物体GT生成是必要的。

**objectGT目录下的GT是combined_new.obj，其他都是GT合成的中间产物，请不要错用！！！！**

### CHAIRS相机参数

**<font color='blue'> 悬而未解，等我再看看或者还有高手。。。。。。</font>**
