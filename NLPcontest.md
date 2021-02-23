# NLPcontest

> some note used in the NLPcontest

link of contest :[**全球人工智能技术创新大赛**热身赛二: 中文预训练模型泛化能力挑战赛](https://tianchi.aliyun.com/competition/entrance/531865/introduction)

---

## 学习资料

* [踩坑记录——记一次训练提交baseline全过程](https://blog.csdn.net/weixin_40807714/article/details/113856151)
* [比赛全流程体验--datawhale](https://github.com/finlay-liu/tianchi-multi-task-nlp/blob/main/README.md#%E6%AF%94%E8%B5%9B%E5%85%A8%E6%B5%81%E7%A8%8B%E4%BD%93%E9%AA%8C)

## 疑问记录

---

什么是PyTorch?:b站，官网？





## 全流程体验

---

### 下载Bert全权重

* [**Hugging Face**](https://huggingface.co/)如何clone 仓库：powershell 到达文件夹输入`git clone https://huggingface.co/bert-base-chinese`

  >How to use from the [🤗/transformers](https://github.com/huggingface/transformers) library:

  

  ```
  from transformers import AutoTokenizer, AutoModelForMaskedLM
  
  tokenizer = AutoTokenizer.from_pretrained("bert-base-chinese")
  
  model = AutoModelForMaskedLM.from_pretrained("bert-base-chinese")
  ```

  ### Or just clone the model repo

  ```
  git lfs install
  git clone https://huggingface.co/bert-base-chinese
  
  # if you want to clone without large files – just their pointers
  # prepend your git clone with the following env var:
  
  GIT_LFS_SKIP_SMUDGE=1
  ```
  * 遇到的问题1：warning: Clone succeeded, but checkout failed.
    * 处理：没有发现有什么影响，文件已经下载成功了
  * 问题2：两个大文件没有clone 下来，手动下载，使用xdown下载很快
    * pytorch_model.bin
    * tf_model.h5

* config.json vocab.txt pytorch_model.bin，把这三个文件放进tianchi-multi-task-nlp/bert_pretrain_model文件夹下。

### 数据集下载

使用powershell 快速创建文件夹

## 3分开训练集和验证集

* 直接forker [比赛全流程体验--datawhale ](https://github.com/finlay-liu/tianchi-multi-task-nlp/blob/main/README.md#%E6%AF%94%E8%B5%9B%E5%85%A8%E6%B5%81%E7%A8%8B%E4%BD%93%E9%AA%8C)

* 然后clone 到本地

  > 如何取消本地仓库，删除.git 文件夹。
  >
  > 如何在文件管理器中查看.git 文件夹，文件资源管理器“查看”-》“隐藏的项目”

* 文件移动

> note:之前是先clone到本地，然后文件都已经放进文件夹。但是后来想到fork之后可以同步到自己的同步，可以存储修改。于是：1.删除了原来的所有文件夹2.重新clone。 但是：后来想到可以不删除，直接forker 之后再push也可以

* 运行

```python
python ./generate_data.py
```

问题：

```
-------------------------------start-----------------------------------
Traceback (most recent call last):
  File "./generate_data.py", line 91, in <module>
    split_dataset(dev_data_cnt=3000)
  File "./generate_data.py", line 20, in split_dataset
    for line in f:
UnicodeDecodeError: 'gbk' codec can't decode byte 0xaf in position 6: illegal multibyte sequence
```

所有的with open 都加上 encoding='utf-8'

问题2：本地没有GPU运行，学习云端的如何使用？

* 看直播视频

  > 天池竞赛docker快速复现：
  > 录播地址：https://www.bilibili.com/video/BV1jy4y1J7rp/
  > 视频材料链接：https://pan.baidu.com/s/1LWcYRa4cpz5AkDeTeebqvg 
  > 提取码：1234 
  > ------------------------------
  > 天池nlp预训练泛化挑战Baseline：
  > 录播地址：https://www.bilibili.com/video/BV1Yz4y127FM/
  > 视频材料链接：链接：https://pan.baidu.com/s/13QPXvfryu6sXopJQ04gFnA 
  > 提取码：1234 

* [学习google 的python 怎么用](https://cloud.google.com/ai-platform/training/docs/using-gpus?hl=zh-cn)

## 4.提交

日期:2021-02-23 10:37:16排名: 无[查看日志](https://tianchi.aliyun.com/competition/examinelog/531865/723/443409/1286355?isTcc=true&scoreId=1577767)

score:0.6172

score_ocnli:0.7010

score_tnews:0.6867

score_ocemotion:0.4639