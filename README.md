# danmaku-text-analysis
bilibili弹幕文本分析
### bilibili爬虫
+ 通过requests模块实现
+ 弹幕路径：https://api.bilibili.com/x/v1/dm/list.so?oid=[cid]
[cid]为https://api.bilibili.com/x/player/pagelist?bvid=BV-----&jsonp=jsonp中json的cid对应的value
连接中的BV-----为b站视频的BV号
+ 存储弹幕：将每个视频下的全部弹幕转化为一个dataframe，存储为csv格式
+ 抓取相关列表中的视频（实验中每个起点抓取了50-80个视频，都没有爬出原本的分类）
### 弹幕文本分析
#### 基于sklearn分类
+ jieba分词
+ 停用词：baidu_stopwords(https://github.com/goto456/stopwords)
+ 基于sklearn进行词向量化，生成TF模型
+ 正则匹配同类词，如“哈哈哈”与“哈哈哈哈哈哈”等等
+ 使用sklearn中的分类器进行分类（分类的标签为上一步中每个起始链接视频的分区）
### 基于情感词典的情感分析
+ 基于BosonNLP情感词典(https://bosonnlp.com) 现在进不了官网了，好像变成阿里内部资源了hhh
+ 直接对jieba分词后的词进行打分
+ 对每条弹幕的分数求和得到弹幕情感得分（但结果并不太准确，情感词典的词虽然多但是和弹幕中的常用词相差较大）
