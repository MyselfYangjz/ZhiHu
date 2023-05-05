知乎爬虫
=========
项目wotfuk
------
这个爬虫用实验室十台电脑一起干活，可随时添加删除机器，具有良好的伸缩性，为了能够实现断点续爬和多台电脑之间的协作使用了Redis作队列，
为了保证不重复爬取使用Redis作hash表,所有爬取的任务都放到hash表中进行标记。（打算用布隆过滤器改进，更新时间待定！）
爬取太频繁会被知乎返回429（too many request）,应对的策略是挂代理，一种方法是使用专业的云代理服务（有点贵）,另一种是[自建代理池](https://github.com/wangqifan/ProxyPool)，定时爬取互联网上免费代理ip。最后数据使用sql server存储，
最后对数据进行分析，使用[百度echart.js](http://echarts.baidu.com/)进行画图

所用技术
--
 * 数据库
    * ms sqlserver
    * Redis
 * 数据库访问
   * Entity Framework
   * ServiceStack.Redis
 * HTML解析
   * HtmlAgilityPack
 * 所用Redis的数据结构
   * 队列(多台电脑之间协作)
   * hash(避免重复爬取) 
 * 数据展示
   * echart.js
   
其他：
------
 * 计划
  打算使用redis的bitmap(Bitmaps并不是实际的数据类型，而是定义在String类型上的一个面向字节操作的集合。因为字符串是二进制安全的块，他们的最大长度是512M，最适合设置成2^32位)当bitarray的过滤数组，
 * 可行性分析：
   在使用8个哈希函数的情况下，512MB大小的位数组在误报率万分之五的情况下可以对约两亿的url去重。两个亿的url是足够用的。而且比hash节省大量的空间。（
  先占一个坑，等待我日后更新，先star我的项目吧） <br>
  [布隆过滤器的实现](https://github.com/wangqifan/BloomFilter)
  
数据展示：
---------


<image src="https://github.com/wangqifan/ZhiHu/blob/master/814953-20170108120707706-1003815196.png" width=500>
   
<image src="https://github.com/wangqifan/ZhiHu/blob/master/814953-20170108120724034-1950593592.png" width=500>
<image src="https://github.com/wangqifan/ZhiHu/blob/master/814953-20170108120919675-1582035152.png" width=500>
<image src="https://github.com/wangqifan/ZhiHu/blob/master/814953-20170108121032566-1417590158.png" width=500>
 
 
备注
------

[博客](http://www.cnblogs.com/zuin/)<br>
[本人项目自建代理池](https://github.com/wangqifan/ProxyPool)<br>
[本人项目布隆过滤器](https://github.com/wangqifan/BloomFilter)<br>
如果需要运行程序  请装好Redis，sqlserver  并配置好
欢迎给我的项目提交代码
