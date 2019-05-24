## 爬取知乎问题下的答案图片
#### 1. 安装库
htmlparser用来解析html。

Beautiful Soup 是一个可以从 HTML 或 XML 文件中提取数据的 Python 库。

> pip install beautifulsoup4

Selenium 是浏览器自动化测试框架，使用它来模拟用户操作。

利用 pip 安装 selenium
> pip install -U selenium




#### 2. 模拟用户进行滚动和点击操作

使用JS控制滚动条的位置：

> window.scrollTo(x,y);

竖向滚动条置底
```
 window.scrollTo(0,document.body.scrollHeight)
 time.sleep(2)
```
向下滑动后延迟两毫秒等待页面加载。

在页面上通过审查，找到**查看更多回答**的html代码
```
<button class="Button QuestionMainAction"
type="button">查看更多回答</button>
```
通过                
```
driver.find_element_by_css_selector('button.QuestionMainAction').click()
```

来选中并点击这个按钮。

#### 3. html文件结构化

将html文件结构化并保存，原页面的html解析并存储下来

通过prettify()将html结构化，之后存储在本地的txt文件中。

#### 4. 保存并下载图片


注意我们的目的，就是爬取回答下的图片，其他的都不需要。

还是右键审查，可以发现每张图片上面都有<noscript>的node，没错，这里面存有图片的高清URL和缩略图URL。

每个<noscript>元素都被html entity编码了，所以我们要将其解码如下。

> html.parser.unescape

之后就可以将图片URL保存下来。

最后下载图片。

>  urllib.request.urlretrieve


#### 5. 结果展示
![image](https://github.com/stevenling/Crawling-zhihu-answer/raw/master/image/1.png)

![image](https://github.com/stevenling/Crawling-zhihu-answer/raw/master/image/2.png)

![image](https://github.com/stevenling/Crawling-zhihu-answer/raw/master/image/3.png)


