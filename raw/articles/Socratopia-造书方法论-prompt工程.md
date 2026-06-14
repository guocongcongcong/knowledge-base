---
title: "Socratopia 造书方法论：用 Prompt 生成教材的全流程"
source: 知乎 吴乐旻
url: https://www.zhihu.com/question/2037704515659543418/answer/2037720895192559755
created: 2026-06-14
type: article
tags: [Socratopia, AI教育, prompt-engineering, 教材生成, 音乐鉴赏]
---

# Socratopia 造书方法论

作者：吴乐旻

## 造书的核心

造书，最关键的，是好点子。

Socratopia发布之后，越来越多的用户不满足于书城和自己手头的教材，想要自己造书。v1.0.7 更新中，FAQ介绍了造书窍门（markdown格式、不要添加目录和引言等）。

## 案例：《细听·古典卷》的诞生

作者拿古典音乐鉴赏教材举了一个完整的例子，展示了从灵感到成书的全部过程。

### 灵光一闪

刚造完计算机专业的十六本新教材后，突然想到：音乐鉴赏！以前总想着让Socratopia教理科的东西，但音乐鉴赏其实和Socratopia完美契合。每一章围绕一段或几段古典音乐，教材让学习者先去YouTube上搜这段音乐去听，然后和虚拟伙伴聊轶事掌故、情绪感情、音乐技术。

音乐鉴赏可以做成整整一个系列的教材：古典音乐外，还有中国民乐、爵士、乡村、摇滚、甚至周杰伦作品鉴赏。

### 为什么 Socratopia 是天选载体

- **音乐鉴赏的本质是"听 + 聊"，不是"听 + 测验"。**书 + 虚拟伙伴 = 把"有一个懂音乐的朋友陪你听"变成可扩展的产品形态。
- **音乐欣赏门槛极低、深度无限。**任何水平的学习者都能从陪伴体的同一段素材里抽出对自己有用的层次。
- **YouTube已经是全球音乐图书馆。**书不需要附带音频，搜索hint就够——天然轻量。
- **作品池是finite且已稳定**（古典曲目几百年没变），适合教材结构化处理。

### Claude的补充设计思路

**关于链接：**不写死URL，只给"搜索hint"。URL会失效，搜索hint不会。而且指明推荐的演奏版本本身就是教学——同一首曲子卡拉扬和克莱伯是两个宇宙。

**章节四段结构：**
1. Before You Listen（30秒预热）——这首多长、写于什么时候、特别注意什么（最多3件事）
2. The Listening Window——听完后"再听一遍"的提示（二刷是关键）
3. What's Happening in the Music——结构地图、关键时刻、技术亮点
4. The Stories——轶事掌故（Socratopia伙伴的弹药库，承担每章半小时聊天素材密度）

**读者定位：**"喜欢听但不识谱"的业余爱好者。不要求读谱，形式概念逐步引入，不预设音乐史脉络。

**轶事密度是教学心脏：**贝多芬聋了之后指挥第九、《春之祭》1913首演引发斗殴、肖斯塔科维奇五号是不是给斯大林的"道歉"——这些是主菜，不是装饰。

### 系列命名

系列名：**Close Listening（细听）**
各卷：《细听·古典卷》、《细听·爵士卷》……

### 最终 Prompt

文中给出了完整的 textbook generation prompt，包含：定位、Anti-Definition、读者、4条关键要求、Threading（作曲家群像6-8位 + 要丢掉的6个习惯 + Dies Irae跨世纪线索）、约27章/9部分结构、Voice DNA（15个来源音色）、约30首主作品+30-50首穿插、编辑规范（YouTube搜索hint约定）、风险与开放问题等。

Prompt 声调定义：
> "Bernstein, on the first of his Young People's Concerts in 1958, said: 'I want to do music for you that I really love, music that I want to share with you. And we'll talk about it together.' Sixty-eight years later, the project is the same. The medium is different. The voice is the same."
