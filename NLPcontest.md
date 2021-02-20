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



？？？对哦，自己连NLP是啥好像都不懂。。去找找教程，等等，因该和之前的神经网络和觉错树差不多，调用一个函数？？先看一下是不是要用第一个下载的包，看看怎么用，找找教程

> >1. 分开训练集和验证集，默认验证集是各3000条数据，参数可以自己修改：
> >
> >```
> >python ./generate_data.py
> >```
> >
> >1. 训练模型，一个epoch：
> >
> >```
> >python ./train.py
> >```
> >
> >会保存验证集上平均f1分数最高的模型到 ./saved_best.pt
> >
> >1. 用训练好的模型 ./saved_best.pt 生成结果：
> >
> >```
> >python ./inference.py
> >```
> >
> >1. 打包预测结果。
> >
> >```
> >zip -r ./result.zip ./*.json
> >```