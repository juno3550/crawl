# crawler
 多线程爬虫


thread_image_crawler.py（多线程+队列：爬取某网站所有图片）

实现框架：
* download_image(url, image_dir, image_no)：将图片下载页的主图下载到本地。
* get_image_url(url)：拼接图片下载的url（绝对路径）。由于网站中的图片src都是相对路径，因此需要在此函数中拼接图片的绝对路径。
* get_page_url(url)：获取图片浏览页中的图片下载页url和翻页url。
* task(queue)：多线程的任务函数，以调用上述3个函数。


thread_keyword_crawler.py（多线程+队列+入库：根据关键字筛选爬取网页）

实现思路：
多线程爬取网页信息，从一个页面为起点，爬取其包含的所有链接，并根据关键字筛选，将符合的网页入库。
1. 访问首页（种子页），获取源码 html；
2. 使用正则或者其他方式获取所有的绝对地址链接，存到一个 list 里面；
3. 遍历 list，加入到队列中；
4. 多线程从队列中取数据，一次取一个绝对地址链接，并重复上面1-3步。

实现框架：
* MysqlTool 类：将 mysql 的初始化及操作进行封装。
* get_page_message()：获取当前网页的所需信息（标题、正文、包含的所有链接）。
* get_html()：多线程任务函数，将包含关键字的当前页面进行入库，并将包含的所有链接放入队列中，以此循环。
