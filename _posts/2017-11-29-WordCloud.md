---
layout: post
title: 学习笔记-Python生成词云WordCloud
date: 2017-11-29
img: HuazhuWords.jpeg 
tags: [Blog, NLP]
---

之前在浏览一些数据分析的文章的时候，发现有一个叫WordCloud(词云)的东西很有意思。

以下是我在博客园搜索时找到的一个简短有效的python3代码：(原文链接：http://www.cnblogs.com/franklv/p/6995150.html)

```
#encoding=gbk #中文编码

import jieba.analyse
from PIL import Image,ImageSequence
import numpy as np
import matplotlib.pyplot as plt
from wordcloud import WordCloud,ImageColorGenerator
lyric= ''
f=open('Scala.txt','r') #有些组织的不好的文件运行效果不好
for i in f:
    lyric+=f.read()
    
#这里是使用jieba进行分词，会挑选出频率最高的词(默认前20个)
result=jieba.analyse.textrank(lyric,topK=50,withWeight=True)
keywords = dict()
for i in result:
    keywords[i[0]]=i[1]
#print(keywords)

#这里的img是你要使用的图片模板，形状颜色什么的就靠它啦
image= Image.open('./tim.png')
graph = np.array(image)
wc = WordCloud(font_path='./fonts/simhei.ttf',background_color='White',max_words=50,mask=graph)
wc.generate_from_frequencies(keywords)
image_color = ImageColorGenerator(graph)
plt.imshow(wc)
plt.imshow(wc.recolor(color_func=image_color))
plt.axis("off")
plt.show()
wc.to_file('dream.png')
```

这里是我的输出结果。好像还可以哈：

<img width="550" src="{{ site.baseurl }}/assets/img/dream.png">

最后贴上一个超好的词云制作网站，亲测有效，快去制作你自己的词云吧：
https://wordart.com/create
