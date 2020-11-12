# jieba分词
## 测试文段
```
我们创立于1958年，致力于在世界各地拓展商业范围，现已成为一家领先的商业机械进出口承包商。
现在，我们有志于以贵方市场为基础，向欧洲拓展商业贸易。
如你方能推荐一可靠的商业机器进口承包商，我方将不胜感激。
我们的业务内容包括打字机、复印机、打印机以及收音机等。
如您对我方的财务状况以及声誉有疑问，请至中国银行处垂询。
我们非常感谢您的配合。
期待很快收到您的回信。
我方已开立以你方为受益人的不可撤销信用证第487号，价值6936英镑，有效期至11月30日。
贵方现可以在该信用证下，依据发票金额见票60日提款。
如贵方能够履行信用证中提及条款，我方愿意于到期时支付在该信用证下的各项汇票。
```
## 无字典分词
### 结果
![ktzy07_1 pic](https://github.com/JayKay7812/Database-Theory-2/blob/master/%E8%AF%BE%E5%A0%82%E4%BD%9C%E4%B8%9A07/img/ktzy07_1.png)
### 代码
```
import jieba

f1 = open("zh_tokenize_test.txt", "r",encoding='UTF-8')

for line in f1.readlines():
    line=line.strip()
    word_list=jieba.cut(line,cut_all=False)
    print("/".join(word_list),"\n")

f1.close()
```
## 有字典分词
### 字典
```
你方
不可撤销信用证
见票60日
商业机械

```
### 结果
![ktzy07_2 pic](https://github.com/JayKay7812/Database-Theory-2/blob/master/%E8%AF%BE%E5%A0%82%E4%BD%9C%E4%B8%9A07/img/ktzy07_2.png)
### 代码
```
import jieba

jieba.load_userdict("zh_dict.txt")

f1 = open("zh_tokenize_test.txt", "r",encoding='UTF-8')

for line in f1.readlines():
    line=line.strip()
    word_list=jieba.cut(line,cut_all=False)
    print("/".join(word_list),"\n")

f1.close()

```

# nltk分词
## 测试文段
```
Established in 1958，we have been expanding our business operations around the world as a leading exporter and importer of business machines .
Now we are planning to incorporate our business activities in your market as general base in Europe.
We will be much obliged for your introduction to a most reliable importer handling business machine.
Our line of business includes: Typewriter, Copying Machines, Printing Machines, Cash Register, etc..
Considering our financial status and reputation, please direct all inquiries to the Bank of China.
Thank you very much for your corporation.
We hope to hear from you very soon.
We have opened an irrevocable L/C No.487 for ￡6,936 in your favor， valid until 30 November.
You have authority to draw on us at 60d/s against this credit for the amount of your invoice.
Provided you fulfill the terms of the credit we will accept and pay at maturity the drafts presented to us under this credit.

```
## 无字典分词
### 结果
![ktzy07_3 pic](https://github.com/JayKay7812/Database-Theory-2/blob/master/%E8%AF%BE%E5%A0%82%E4%BD%9C%E4%B8%9A07/img/ktzy07_3.png)
### 代码
```
import nltk
from nltk.tokenize import word_tokenize
from nltk.tokenize import MWETokenizer

f2 = open("en_tokenize_test.txt", "r",encoding='UTF-8')

tokenizer=MWETokenizer([('Bank','of','China'),('irrevocable','L/C'),('business','machines'),('Copying','Machines'),('Printing','Machines'),('Cash','Register')],separator='_')

def preprocess(sent):
    sent = nltk.word_tokenize(sent)
    return sent

for line in f2.readlines():
    line=line.strip()
    word_list=preprocess(line)
    print(word_list,"\n")

```
## 有字典分词
### 结果
![ktzy07_4 pic](https://github.com/JayKay7812/Database-Theory-2/blob/master/%E8%AF%BE%E5%A0%82%E4%BD%9C%E4%B8%9A07/img/ktzy07_4.png)
### 代码
```
import nltk
from nltk.tokenize import word_tokenize
from nltk.tokenize import MWETokenizer

f2 = open("en_tokenize_test.txt", "r",encoding='UTF-8')

tokenizer=MWETokenizer([('Bank','of','China'),('irrevocable','L/C'),('business','machines'),('Copying','Machines'),('Printing','Machines'),('Cash','Register')],separator='_')

def preprocess(sent):
    sent = tokenizer.tokenize(nltk.word_tokenize(sent))
    return sent

for line in f2.readlines():
    line=line.strip()
    word_list=preprocess(line)
    print(word_list,"\n")

```
