---
layout: post
title: 学习笔记-使用爬虫爬取花千骨小说
date: 2017-10-29
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: post-6.jpg # Add image post (optional)
tags: [Blog, Python]
author: # Add name author (optional)
---

参考药少敏博客：https://segmentfault.com/a/1190000010783635

```python
from urllib import request
from bs4 import BeautifulSoup

if __name__ == '__main__':
    # 第8章的网址
    url = 'http://www.136book.com/huaqiangu/ebxeew/'
    head = {}
    # 使用代理
    head['User-Agent'] = 'Mozilla/5.0 (Linux; Android 4.1.1; Nexus 7 Build/JRO03D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166  Safari/535.19'
    req = request.Request(url, headers = head)
    response = request.urlopen(req)
    html = response.read()
    # 创建request对象
    soup = BeautifulSoup(html, 'lxml')
    # 找出div中的内容
    soup_text = soup.find('div', id = 'content')
    # 输出其中的文本
    print(soup_text.text)
```

    
    　　“骨头，你知道这世间有哪六界么？”　　花千骨看着他的脸发呆，这人笑起来怎么会这生好看，暖融融的让她好想睡觉哦！　　“呃……人的世界，鬼的世界，妖魔的世界，还有神仙的世界？还有什么？”她扳起手指头来数，好像不够。　　“差不多就是这几个，人界，冥界，妖界，魔界，仙界，还有神界。”　　“哇，分这么详细啊……那冥界、妖界、魔界代表恶，人界、仙界、神界代表善对吧？两者相互制衡？清虚道长说的妖神要出世，是不是说妖界的最厉害的怪物要跑出来了？怪不得我看最近大白天的多了那么多妖怪。”　　“六界并不是这么简单的善恶问题。人死为鬼入冥界，修炼的话成仙能位列仙班，而妖比较复杂，一般是自然物化的结果，动物，植物，甚至器皿由于自身或者外力的原因都有可能成精，形态更是千奇各异。至于魔界，不管是人也好，妖也好，仙也好，恶意、执念、天劫、练功走火皆有可能堕入魔道。”　　“那神呢？人们总说神仙神仙，我一直以为神和仙是一个东西”　　“上古众神与天地同生，而仙一般都是修炼而成，虽都有法力，但是并不一样。只是人们爱把他们说在一块，就好像爱把妖和魔，合起来说成妖魔一样。伏羲演八卦，女娲造人，西王母的蟠桃会，共工撞倒不周山，夸父逐日，精卫填海，仓颉造字，黄帝大战蚩尤，这些传说你都应该听过。只是，神仙妖魔虽然通过修炼可以长生不老，但都并不是不死之身。有的可以入轮回，到冥界进行投胎或转生，但是大多数都是直接寂灭。”　　“说来说去，还是做人最苦最难啊！”　　“非也，世间人的数量是最多的，其他族类只是很小一部分。人界看似最没有能力，其实是最强大的一个界，更是六界之源，万物之根本。”　　“没发现做人强在哪好在哪啊？”　　“人心的力量才是最强大的，你以后就会懂。而追求做人的更高层次，并不一定是做仙。所以你也没必要如此执着的去拜什么师、求什么道、修什么仙，不管是神仙还是妖魔，都各有各的烦恼，说不定还没做人来得简单快乐。”　　花千骨觉得很有理的点点头。　　“那清虚道长他们算是人还是仙呢？一开始他让我去参加什么群仙会我还想不通，我一个普通人，怎么去得了。”　　“你没有看他给你的那个《六界全书》么？里面分类还有级别等应该都叙述的十分清楚。”　　“还没有看，下月十三就是群仙宴了，到昆仑山那么远，我怕赶不上，这些天拼命的赶路，晚上一躺下就睡着了，根本就忘了那书的事了。”　　“仙的等级依照法力和地位的不同一般可以分成九品：第一上仙，第二次仙，第三太上真人，第四飞天真人，第五灵仙，第六真人，第七灵人，第八飞仙，第九仙人。成仙的方式也有许多种，主要是佛道两家，通过修佛和修道两种途径。另外还有天仙，地仙和尸解仙等等，就是先死再成仙。还有通过外力吃仙药灌输仙力等方法，当然自己修炼白日飞升或者直接成仙是最好的。”　　“哦，原来长留上仙是这么厉害的啊？”　　“什么！？”东方彧卿眯起眼睛。　　“清虚道长让我去拜长留上仙白子画为师。”　　东方彧卿冷哼一声，温暖的眼睛突然变得有些倨傲，不知道为什么花千骨会突然觉得他有点熟悉。　　“他们都成仙了，还会管这世俗中的事，还会收徒弟么？”以前她总感觉仙人是高高在上，很难见到的。　　“如今这个世道，妖魔猖狂，得道成仙者和修真者之间几乎已经没什么太大界限了，除了天庭位于九天之上，其他成仙者，不管是有封位还是闲云野鹤的散仙，多居于山野桃源，海外仙岛的洞天福地，世人都可以去访仙求缘。说穿了，仙人根本没有世人所描述的那样高高在上，不可亵渎。只不过是比平常人多些法力，少点情欲罢了。一个偏颇，反而比人更容易堕入魔道。”　　花千骨听他话里隐隐对仙人的不屑，一时不知道说什么好。那她的未来师父是个什么样的人呢？　　“那清虚道长应该也是上仙吧？”　　“他？应该是真人吧，你以为成仙那么容易？整个仙界现在上仙也不过仅余寥寥四人。”　　“哇，那么厉害！我以为成仙了的肯定都是什么去了西方极乐啊什么的。”　　“大部分仙都不愿意留在天庭受各种天规天条管制，白日飞仙之后或是去六界游仙，或是留在以前修道的地方，继续培养弟子飞仙。这次万年轮回妖神出世实在是无可避免，仙界又怎么可能没有防备。所以从很多年前就在拼命的扩大剑仙和修道者的队伍，以对付那些横空出世的妖魔。各仙都在拼命光大自家门派，招收弟子，以求仙魔大战中能够自保，茅山便是其中之一。另外还有王屋山，崂山，太白，蓬莱等等……多不胜数，稍有些仙资的，便都被收了去。”　　“女孩也可以么？”　　“大部分门派都收女弟子，道法还有男女双修的。少数一些特例是因为本门仙术只适合男子，就连茅山也是时常会收女弟子的。”　　“啊，那太好了！长留山也收的吧？那我拜师成功的几率又大增加了！”　　东方彧卿看她兴奋的样子不由得扬嘴一笑。　　“长留山是所有门派中最大也是最好的修道之所，门下弟子也是最多的。其他各门派的优秀弟子，也会定期往那里推荐派送。现今世上三分之一的得道者都是从那里出来，那里的仙术道法齐全，囊括百家之所长，法术高的仙人也比最多，几乎整个仙界都望其项背。”　　顿了顿，又道：“不过当然，最重要的还是因为掌门是个连玉帝都不敢得罪的长留上仙白子画。”　　花千骨一听更加紧张了。　　“他很厉害很难相处么？”　　“厉害是一定的，仙界有真材实料的不多，论对手，他绝对是最可怕的一个。要说难相处，谣言并不可信，你自己去了就知道了。虽然我不喜欢他，可你若真能拜到他为师，的确是几世修来的福气。”　　花千骨越发佩服东方彧卿了。这人怎么什么都知道啊！真的只是普通的书生么？　　“听你说的好像见过他似的。”　　“当然没见过，我哪有那本事。我虽然博学识广，却只会纸上谈兵。你若是有不知道的事可以来问我，忙我就帮不上什么了。”　　“那如果他不肯收我为徒的话，我有没有什么办法可以求他啊？”　　“人心的事我可说不准，你就自求多福吧！”　　“呃……我好紧张，哦，对了，你还没跟我说那个妖神是什么东西？为什么会惹得六界如此大乱？”　　“具体是个什么没有人能说得清楚，之所以称其为妖神，是因为其具有神一样强大的能力和破坏力吧。不但吸取了数万年的日月精华，而且也融合了世间一切邪恶，丑陋，仇恨，战争，私欲等不好的东西于一体，然后物化成妖。出世的同时，妖界，冥界，魔界都会洞门大开，人间兵伐不断，天灾不止，百姓民不聊生，世间一切皆会毁灭殆尽。”　　“没有办法制止么？神仙们都那么厉害！”　　“上一次出世的时候制止过一次，最后用十六件上古神器，分别在各个方位把它封印了。但是其本元便是集世上一切邪恶丑陋于一身，只要人心里还有恶念，对其便永无可完全根除之日。积累到一定时间，它总还是要出来为祸人间，毁灭一切。”　　“怪不得那个拴天链那么重要，若是集齐了，妖神不是就复活了么？”　　“正是这样。”　　“那其他的都在哪？”　　“由各个门派作为镇门之宝代代看护。但是总是有一些居心叵测的妖魔想要抢夺，放妖神出世。”　　“长留山也有？”　　“当然。”　　“不过应该没事的，剩下的毕竟还有十五件，不会那么容易集齐的。况且就算妖神真的出世，有那么多神人和仙人在，难道还怕制不住他么？再像上次一样把它封印起来就好了。”　　东方彧卿看着她笑，却不知原本舒服的笑容此刻为何却显得诡异莫名。　　“千骨，这个世界上，已经没有神了！” 
    					document.write('<a style="display:none!important" id="tanx-a-mm_14370482_3424918_15814205"></a>');
    					tanx_s = document.createElement("script");
    					tanx_s.type = "text/javascript";
    					tanx_s.charset = "gbk";
    					tanx_s.id = "tanx-s-mm_14370482_3424918_15814205";
    					tanx_s.async = true;
    					tanx_s.src = "http://p.tanx.com/ex?i=mm_14370482_3424918_15814205";
    					tanx_h = document.getElementsByTagName("head")[0];
    					if(tanx_h)tanx_h.insertBefore(tanx_s,tanx_h.firstChild);
    			
    
    


```python
from urllib import request
from bs4 import BeautifulSoup

if __name__ == '__main__':
    # 目录页
    url = 'http://www.136book.com/huaqiangu/'
    head = {}
    head['User-Agent'] = 'Mozilla/5.0 (Linux; Android 4.1.1; Nexus 7 Build/JRO03D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166  Safari/535.19'
    req = request.Request(url, headers = head)
    response = request.urlopen(req)
    html = response.read()
    # 解析目录页
    soup = BeautifulSoup(html, 'lxml')
    # find_next找到第二个<div>
    soup_texts = soup.find('div', id = 'book_detail', class_= 'box1').find_next('div')
    # 遍历ol的子节点，打印出章节标题和对应的链接地址
    for link in soup_texts.ol.children:
        if link != '\n':
            print(link.text + ':  ', link.a.get('href'))
```

    第1章 天煞孤星:   http://www.136book.com/huaqiangu/ebxeeql/
    第2章 荒山尸骨:   http://www.136book.com/huaqiangu/ebxeerc/
    第3章 拔舌地狱:   http://www.136book.com/huaqiangu/ebxeet/
    第4章 往右歪比往左歪好看:   http://www.136book.com/huaqiangu/ebxeegba/
    第5章 本来就不是男人:   http://www.136book.com/huaqiangu/ebxeej/
    第6章 修罗场(1):   http://www.136book.com/huaqiangu/ebxeek/
    第7章 修罗场(2):   http://www.136book.com/huaqiangu/ebxeez/
    第8章 长留上仙白子画:   http://www.136book.com/huaqiangu/ebxeew/
    第9章 没有神的世界:   http://www.136book.com/huaqiangu/ebxeev/
    第10章 异朽阁的妖精:   http://www.136book.com/huaqiangu/ebxeea/
    第11章 花儿的克星:   http://www.136book.com/huaqiangu/ebxeeb/
    第12章 绝色师父:   http://www.136book.com/huaqiangu/ebxeec/
    第13章 小破孩最不可爱了:   http://www.136book.com/huaqiangu/ebxeed/
    第14章 人间仙境:   http://www.136book.com/huaqiangu/ebxeee/
    第15章 等级制度:   http://www.136book.com/huaqiangu/ebxeef/
    第16章 居然睡着了:   http://www.136book.com/huaqiangu/ebxefxe/
    第17章 女娲石已碎:   http://www.136book.com/huaqiangu/ebxefql/
    第18章 惹毛了:   http://www.136book.com/huaqiangu/ebxefrc/
    第19章 人气排行:   http://www.136book.com/huaqiangu/ebxeft/
    第20章 只争朝夕:   http://www.136book.com/huaqiangu/ebxefgba/
    第21章 月夜焚香:   http://www.136book.com/huaqiangu/ebxefj/
    第22章 茅山掌门:   http://www.136book.com/huaqiangu/ebxefk/
    第23章 血红的眸子:   http://www.136book.com/huaqiangu/ebxefz/
    第24章 可爱骨头:   http://www.136book.com/huaqiangu/ebxefw/
    第25章 风涯无边:   http://www.136book.com/huaqiangu/ebxefv/
    第26章 绝贪，绝欲，绝情:   http://www.136book.com/huaqiangu/ebxefa/
    第27章 仙剑大会:   http://www.136book.com/huaqiangu/ebxefb/
    第28章 背海一战:   http://www.136book.com/huaqiangu/ebxefc/
    第29章 最后一搏:   http://www.136book.com/huaqiangu/ebxefd/
    第30章 命中注定的事(1):   http://www.136book.com/huaqiangu/ebxefe/
    第31章 命中注定的事(2):   http://www.136book.com/huaqiangu/ebxeff/
    第32章 俯瞰千山:   http://www.136book.com/huaqiangu/ebqlxexe/
    第33章 一年背七本:   http://www.136book.com/huaqiangu/ebqlxeql/
    第34章 古琴:   http://www.136book.com/huaqiangu/ebqlxerc/
    第35章 师父也要洗澡的么:   http://www.136book.com/huaqiangu/ebqlxet/
    第36章 沧海笑傲:   http://www.136book.com/huaqiangu/ebqlxegba/
    第37章 我欲成仙:   http://www.136book.com/huaqiangu/ebqlxej/
    第38章 美人出浴:   http://www.136book.com/huaqiangu/ebqlxek/
    第39章 丹青难描:   http://www.136book.com/huaqiangu/ebqlxez/
    第40章 七月十四鬼门开:   http://www.136book.com/huaqiangu/ebqlxew/
    第41章 比较衰:   http://www.136book.com/huaqiangu/ebqlxev/
    第42章 二鬼斗法:   http://www.136book.com/huaqiangu/ebqlxea/
    第43章 兵戎相见:   http://www.136book.com/huaqiangu/ebqlxeb/
    第44章 琴魔大战:   http://www.136book.com/huaqiangu/ebqlxec/
    第45章 美人魔君:   http://www.136book.com/huaqiangu/ebqlxed/
    第46章 神器之战:   http://www.136book.com/huaqiangu/ebqlxee/
    第47章 无心无情的白子画:   http://www.136book.com/huaqiangu/ebqlxef/
    第48章 暗影浮香:   http://www.136book.com/huaqiangu/ebqlqlxe/
    第49章 身中剧毒:   http://www.136book.com/huaqiangu/ebqlqlql/
    第50章 还有哪儿没看过么:   http://www.136book.com/huaqiangu/ebqlqlrc/
    第51章 本能还是心意:   http://www.136book.com/huaqiangu/ebqlqlt/
    第52章 皓月邯郸:   http://www.136book.com/huaqiangu/ebqlqlgba/
    第53章 又傻又卑微地爱慕着:   http://www.136book.com/huaqiangu/ebqlqlj/
    第54章 再赴瑶池:   http://www.136book.com/huaqiangu/ebqlqlk/
    第55章 酒能忘忧:   http://www.136book.com/huaqiangu/ebqlqlz/
    第56章 见师父，腿发软:   http://www.136book.com/huaqiangu/ebqlqlw/
    第57章 情意暗长:   http://www.136book.com/huaqiangu/ebqlqlv/
    第58章 在劫难逃 (1):   http://www.136book.com/huaqiangu/ebqlqla/
    第59章 在劫难逃 (2):   http://www.136book.com/huaqiangu/ebqlqlb/
    第60章 生死与共:   http://www.136book.com/huaqiangu/ebqlqlc/
    第61章 情意败露:   http://www.136book.com/huaqiangu/ebqlqld/
    第62章 孽障东西(1):   http://www.136book.com/huaqiangu/ebqlqle/
    第63章 孽障东西(2):   http://www.136book.com/huaqiangu/ebqlqlf/
    第64章 什么都可以给你:   http://www.136book.com/huaqiangu/ebqlrcxe/
    第65章 有口难言:   http://www.136book.com/huaqiangu/ebqlrcql/
    第66章 命悬一线:   http://www.136book.com/huaqiangu/ebqlrcrc/
    第67章 惊天一吻:   http://www.136book.com/huaqiangu/ebqlrct/
    第68章 最美好的记忆:   http://www.136book.com/huaqiangu/ebqlrcgba/
    第69章 曲终人散:   http://www.136book.com/huaqiangu/ebqlrcj/
    第70章 盗取神器:   http://www.136book.com/huaqiangu/ebqlrck/
    第71章 可怕的怪物:   http://www.136book.com/huaqiangu/ebqlrcz/
    第72章 没人可以活过二十五岁:   http://www.136book.com/huaqiangu/ebqlrcw/
    第73章 朔风的脸(1):   http://www.136book.com/huaqiangu/ebqlrcv/
    第74章 朔风的脸(2):   http://www.136book.com/huaqiangu/ebqlrca/
    第75章 大闹东海:   http://www.136book.com/huaqiangu/ebqlrcb/
    第76章 身世之迷:   http://www.136book.com/huaqiangu/ebqlrcc/
    第77章 一触即发:   http://www.136book.com/huaqiangu/ebqlrcd/
    第78章 妖神出世:   http://www.136book.com/huaqiangu/ebqlrce/
    第79章 花月洞天:   http://www.136book.com/huaqiangu/ebqlrcf/
    第80章 谁是妖神:   http://www.136book.com/huaqiangu/ebqltxe/
    第81章 冰火相峙:   http://www.136book.com/huaqiangu/ebqltql/
    第82章 二吻真言:   http://www.136book.com/huaqiangu/ebqltrc/
    第83章 触目惊心的血迹(1):   http://www.136book.com/huaqiangu/ebqltt/
    第84章 触目惊心的血迹(2):   http://www.136book.com/huaqiangu/ebqltgba/
    第85章 用心良苦:   http://www.136book.com/huaqiangu/ebqltj/
    第86章 腐心蚀骨(1):   http://www.136book.com/huaqiangu/ebqltk/
    第87章 腐心蚀骨(2):   http://www.136book.com/huaqiangu/ebqltz/
    第88章 蛮荒雾泽:   http://www.136book.com/huaqiangu/ebqltw/
    第89章 决绝狠毒到如此地步:   http://www.136book.com/huaqiangu/ebqltv/
    第90章 不可不防:   http://www.136book.com/huaqiangu/ebqlta/
    第91章 万兽之王:   http://www.136book.com/huaqiangu/ebqltb/
    第92章 宏图大志:   http://www.136book.com/huaqiangu/ebqltc/
    第93章 瀚海阑干:   http://www.136book.com/huaqiangu/ebqltd/
    第94章 与虎谋皮:   http://www.136book.com/huaqiangu/ebqlte/
    第95章 蛮荒一统:   http://www.136book.com/huaqiangu/ebqltf/
    第96章 三千妖杀:   http://www.136book.com/huaqiangu/ebqlgbaxe/
    第97章 我来接你回家:   http://www.136book.com/huaqiangu/ebqlgbaql/
    第98章 红颜祸水:   http://www.136book.com/huaqiangu/ebqlgbarc/
    第99章 天下人和我你选谁(1):   http://www.136book.com/huaqiangu/ebqlgbat/
    第100章 天下人和我你选谁(2):   http://www.136book.com/huaqiangu/ebqlgbagba/
    第101章 桃花幽若:   http://www.136book.com/huaqiangu/ebqlgbaj/
    第102章 物是人非:   http://www.136book.com/huaqiangu/ebqlgbak/
    第103章 罪孽深重(1):   http://www.136book.com/huaqiangu/ebqlgbaz/
    第104章 罪孽深重(2):   http://www.136book.com/huaqiangu/ebqlgbaw/
    第105章 六十四根消魂钉:   http://www.136book.com/huaqiangu/ebqlgbav/
    第106章 今昔何昔:   http://www.136book.com/huaqiangu/ebqlgbaa/
    第107章 身份败露:   http://www.136book.com/huaqiangu/ebqlgbab/
    第108章 乌龙事件:   http://www.136book.com/huaqiangu/ebqlgbac/
    第109章 报仇雪恨:   http://www.136book.com/huaqiangu/ebqlgbad/
    第110章 全部奉还:   http://www.136book.com/huaqiangu/ebqlgbae/
    第111章 前尘旧怨:   http://www.136book.com/huaqiangu/ebqlgbaf/
    第112章 手感的刺激太过强烈:   http://www.136book.com/huaqiangu/ebqljxe/
    第113章 暧昧不清:   http://www.136book.com/huaqiangu/ebqljql/
    第114章 事出有因:   http://www.136book.com/huaqiangu/ebqljrc/
    第115章 弱水三千:   http://www.136book.com/huaqiangu/ebqljt/
    第116章 至少也给个全尸:   http://www.136book.com/huaqiangu/ebqljgba/
    第117章 镇魂血石:   http://www.136book.com/huaqiangu/ebqljj/
    第118章 南无之月(1):   http://www.136book.com/huaqiangu/ebqljk/
    第119章 南无之月(2):   http://www.136book.com/huaqiangu/ebqljz/
    第120章 惺惺作态的嘴脸:   http://www.136book.com/huaqiangu/ebqljw/
    第121章 仙魔大战:   http://www.136book.com/huaqiangu/ebqljv/
    第122章 总算把初吻送出去了(1):   http://www.136book.com/huaqiangu/ebqlja/
    第123章 总算把初吻送出去了(2):   http://www.136book.com/huaqiangu/ebqljb/
    第124章 师父亲手杀她:   http://www.136book.com/huaqiangu/ebqljc/
    第125章 肝肠寸断:   http://www.136book.com/huaqiangu/ebqljd/
    第126章 心堕魔道，永不翻身:   http://www.136book.com/huaqiangu/ebqlje/
    第127章 万劫不复(1):   http://www.136book.com/huaqiangu/ebqljf/
    第128章 万劫不复(2):   http://www.136book.com/huaqiangu/ebqlkxe/
    第129章 君已陌路:   http://www.136book.com/huaqiangu/ebqlkql/
    第130章 我欠你的，早已还清:   http://www.136book.com/huaqiangu/ebqlkrc/
    第131章 冰心依旧:   http://www.136book.com/huaqiangu/ebqlkt/
    第132章 情潮汹涌:   http://www.136book.com/huaqiangu/ebqlkgba/
    第133章 忆往昔日:   http://www.136book.com/huaqiangu/ebqlkj/
    第134章 人世间有极乐么:   http://www.136book.com/huaqiangu/ebqlkk/
    第135章 一闪而逝的厌恶:   http://www.136book.com/huaqiangu/ebqlkz/
    第136章 又一次伤害她:   http://www.136book.com/huaqiangu/ebqlkw/
    第137章 什么都不在乎了吗:   http://www.136book.com/huaqiangu/ebqlkv/
    第138章 留下她一个人:   http://www.136book.com/huaqiangu/ebqlka/
    第139章 不堪回首:   http://www.136book.com/huaqiangu/ebqlkb/
    第140章 醉生梦死(1):   http://www.136book.com/huaqiangu/ebqlkc/
    第141章 醉生梦死(2):   http://www.136book.com/huaqiangu/ebqlkd/
    第142章 奇耻大辱(1):   http://www.136book.com/huaqiangu/ebqlke/
    第143章 奇耻大辱(2):   http://www.136book.com/huaqiangu/ebqlkf/
    第144章 奇耻大辱(3):   http://www.136book.com/huaqiangu/ebqlzxe/
    第145章 永不分离:   http://www.136book.com/huaqiangu/ebqlzql/
    第146章 朝朝暮暮:   http://www.136book.com/huaqiangu/ebqlzrc/
    第147章 覆水难收:   http://www.136book.com/huaqiangu/ebqlzt/
    第148章 南无豆腐:   http://www.136book.com/huaqiangu/ebqlzgba/
    第149章 情窦又初开:   http://www.136book.com/huaqiangu/ebqlzj/
    第150章 三魂七魄:   http://www.136book.com/huaqiangu/ebqlzk/
    第151章 只有东方一人是真心待她:   http://www.136book.com/huaqiangu/ebqlzz/
    第152章 左右为难:   http://www.136book.com/huaqiangu/ebqlzw/
    第153章 还爱师父么:   http://www.136book.com/huaqiangu/ebqlzv/
    第154章 花好月圆(1):   http://www.136book.com/huaqiangu/ebqlza/
    第155章 花好月圆(2):   http://www.136book.com/huaqiangu/ebqlzb/
    第156章 情深缱绻:   http://www.136book.com/huaqiangu/ebqlzc/
    第157章 番外一：浮生若梦(1):   http://www.136book.com/huaqiangu/ebqlzd/
    第158章 番外一：浮生若梦(2):   http://www.136book.com/huaqiangu/ebqlze/
    第159章 番外二：放手一搏:   http://www.136book.com/huaqiangu/ebqlzf/
    第160章 番外三：长留书院:   http://www.136book.com/huaqiangu/ebqlwxe/
    第161章 番外四：君子好逑(1):   http://www.136book.com/huaqiangu/ebqlwql/
    第162章 番外四：君子好逑(2):   http://www.136book.com/huaqiangu/ebqlwrc/
    第163章 番外五：下手为强:   http://www.136book.com/huaqiangu/ebqlwt/
    第164章 番外六：鹣鲽情深:   http://www.136book.com/huaqiangu/ebqlwgba/
    


```python
from urllib import request
from bs4 import BeautifulSoup

if __name__ == '__main__':
    url = 'http://www.136book.com/huaqiangu/'
    head = {}
    head['User-Agent'] = 'Mozilla/5.0 (Linux; Android 4.1.1; Nexus 7 Build/JRO03D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166  Safari/535.19'
    req = request.Request(url, headers = head)
    response = request.urlopen(req)
    html = response.read()
    soup = BeautifulSoup(html, 'lxml')
    soup_texts = soup.find('div', id = 'book_detail', class_= 'box1').find_next('div')
    # 打开文件
    f = open('C:/Users/changyi/Desktop/huaqiangu.txt','w')
    # 循环解析链接地址
    for link in soup_texts.ol.children:
        if link != '\n':
            download_url = link.a.get('href')
            download_req = request.Request(download_url, headers = head)
            download_response = request.urlopen(download_req)
            download_html = download_response.read()
            download_soup = BeautifulSoup(download_html, 'lxml')
            download_soup_texts = download_soup.find('div', id = 'content')
            # 抓取其中文本
            download_soup_texts = download_soup_texts.text
            # 写入章节标题
            f.write(link.text + '\n\n')
            # 写入章节内容
            f.write(download_soup_texts)
            f.write('\n\n')
    f.close()
```
