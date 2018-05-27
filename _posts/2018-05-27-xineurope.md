---
layout: post
title: 我的博文-新欧洲网站搜索关键词分析
date: 2018-05-27
img: post-xineurope.png
tags: [Blog, NLP]
author: Changyi SONG
---

## 1. 新欧洲和它的搜索序号searchid
新欧洲（http://www.xineurope.com/）网站是非常著名的欧洲华人门户网站。其专栏“跳蚤市场”更是留欧华人不可多得的一个交易平台。买卖二手用品，租房，各种各样的服务都可以在里面找到。不过有一点比较扎心的是，每15秒只能进行一次搜索。

也是机缘巧合，本来博主只是想试一试能否用基础爬虫去抓取里面的内容并加入我的聊天机器人里面。以便之后搜索二手用品的时候方便一点（手动输入了关键词算一次搜索，按时间排序算第二次搜索，排序了发现相关性不高又是第三次搜索。。。）。于是兴冲冲的导入了python里面的Beautifulsoup和urllib等包，尝试静态抓取并修改搜索关键字kw。

'''
from bs4 import BeautifulSoup
import urllib
'''

右键检查页面以后发现我要的关键词kw在一个span标签里面，类型是emfont，于是有了如下代码：

'''
html = urllib.request.urlopen('http://www.xineurope.com/search.php?mod=forum&searchid=935&orderby=lastpost&ascdesc=desc&searchsubmit=yes&kw=').read()
soup = BeautifulSoup(html, "lxml")
keys = soup.find_all('span', {'class': 'emfont'})
'''

但是5秒钟后我懵逼了。那个searchid是个什么鬼？935， 嗯？是不是url弄错了，于是又搜了一次。很惊奇的发现这次的searchid变成了936。

恍然大悟，原来新欧洲网站把每次搜索都编号了，结果其实是看那个id，关键词一旦搜索过了就绑到相应的id了。也就是说，我可以直接通过改id查看我前一个人的搜索记录，前前一个，前前前一个。。。这个还是挺变态的吧！不过还好的是，都是匿名的。所以大家也不必担心自己的搜索结果泄露自己的隐私。

## 2. 数据爬取
其实第一反应，凉了，我的简化爬虫搜索报销了。。。

但转念一想，诶，看看别人的搜索结果，通过数据分析，了解一下大家关注的潮流，貌似也是不错的。于是开始改代码：

'''
html = urllib.request.urlopen('http://www.xineurope.com/search.php?mod=forum&searchid=800&orderby=lastpost&ascdesc=desc&searchsubmit=yes&kw=').read()
soup = BeautifulSoup(html, "lxml")
keys = soup.find_all('span', {'class': 'emfont'})
for j in keys:
	keyWord = j.get_text()
	print(keyWord)
'''

试了一下，嗯不错，还真能看到searchid为800的那位兄台的搜索结果。不过这样的代码太容易出错了，程序员不能给自己挖坑嘛，于是加入异常检测和空值处理，有了如下代码：

'''
from bs4 import BeautifulSoup
import urllib, re, time, multiprocessing

def scraping_xineurope(startId, endId):
    tempId = startId
    key_list = []
    while tempId <= endId:
        try:
            html = urllib.request.urlopen('http://www.xineurope.com/search.php?mod=forum&searchid=' + str(tempId) + '&orderby=lastpost&ascdesc=desc&searchsubmit=yes&kw=').read()
            soup = BeautifulSoup(html, "lxml")
            keys = soup.find_all('span', {'class': 'emfont'})
        except: #这里意思是如果上面三行代码有任何一行执行错误，就会进行另外的异常处理。这里选择的是报错退出
            print('Error happened when scraping search id ' + str(tempId))
            break
        for j in keys:
            keyWord = j.get_text()
            if keyWord: #这里keyWord不存在只有一种情况，就是已经到最新的搜索id了，不能继续了，所以打印提示语句并退出
                key_list.append(keyWord)
                print(str(tempId), keyWord)
            else:
                print('End of search id')
                tempId = endId
        tempId += 1
    print('Scraping from search id ' + str(startId) + ' to search id ' + str(tempId - 1) + ' finished')
    return key_list
	
key_list = scraping_xineurope(1,50)
'''

这样子我们就可以通过startId和endId两个参数来控制我们想爬取searchid为多少号到多少号之间的结果了。很爽的是，搜索历史记录没有两次搜索必须间隔15秒的限制。这里我以1-50为例，看了看大家前50位的都搜了些啥：

'''
1 campus langue
2 里昂 法语
3 lafayette
4 民宿
5 打工
6 峡湾
7 互惠生
8 斯堡
9 互惠生
10 水饺
11 巴黎 民宿
12 打工 拉面
13 16
14 饺子
15 商校认证
16 visiteur转家庭居留
17 换红包
18 rcpc过期
19 巴黎中央理工
20 斯特拉斯堡
...
'''

这里我尝试过多进程爬取。由于貌似本来搜索的结果就没有那么多，也就几百上千个，用多进程爬取反而造成服务器压力大，响应慢。有兴趣的可以自行尝试。

## 3. 词云可视化分析
还是很开心之前接触过一点简单的词云分析，现在就派上用场啦。

思路就是用jieba这个包进行中文分词，然后取出前k个高频词，然后加一张图片按图上的样式画出来就好。完整生成代码如下：

'''
#encoding=gbk #中文编码

import jieba.analyse
from PIL import Image,ImageSequence
import numpy as np
import matplotlib.pyplot as plt
from wordcloud import WordCloud,ImageColorGenerator

lyric= ''
for i in key_list:
    lyric += str(i)
    
#这里是使用jieba进行分词，会挑选出频率最高的词(默认前20个)
result=jieba.analyse.textrank(lyric,topK=50,withWeight=True)
keywords = dict()
for i in result:
    keywords[i[0]]=i[1]
#print(keywords)

#这里的img是你要使用的图片模板，形状颜色什么的就靠它啦
image= Image.open('./obj.png')
graph = np.array(image)
wc = WordCloud(font_path='./fonts/simhei.ttf',background_color='White',max_words=50,mask=graph)
wc.generate_from_frequencies(keywords)
image_color = ImageColorGenerator(graph)
plt.imshow(wc)
plt.imshow(wc.recolor(color_func=image_color))
plt.axis("off")
plt.show()
wc.to_file('res.png')
'''

这样我们就把刚才的爬取结果画出来并保存到名为res的一张png图片里了，就是这样：

<img width="600" src="{{ site.baseurl }}/assets/img/resultXineurope.png">

嗯，就是这样。所以亲们要是猛搜某个关键词，你的词会在中间大大的哦。

完整github代码链接：https://github.com/songchangyi/scraping/tree/master/xineurope

以上。