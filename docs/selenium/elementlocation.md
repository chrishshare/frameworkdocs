# 元素定位方法概览
Selenium元素定位方法总共有八大类，分别是：id，name，class name，tag name，link text，partial link text，xpath，css。  
八种定位方法没有哪个是最好的，在不同的场景下需要使用不用的定位方法。

示例html文件如下：
```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<meta name="referrer" content="origin" />
<title>centos7 部署openstf - ianduin - 博客园</title>
</head>
<body>
    <div>
    <a name="top">猜猜看</a>
	<img alt="点我试试呀" src="/images/bg.jpg">
    <div id="home">
        <div id="cnblogs_post_body" class="blogpost-body">
			<p><span style="line-height: 1.5">openstf项目开源地址：</span></p>
		</div>
		<div class="highlighter-rouge">
			<div class="newsItem">
				<h3 class="catListTitle">公告</h3>
				<div id="blog-news">
					明天也许是个好日子吧
				</div>
			</div>
		</div>
        </div>
    </div>
</body>
</html>
```
# ID定位
* 目标  
根据元素ID找到"明天也许是个好日子吧"所属的元素
* 实现
```python
element1 = driver.find_element_by_id("blog-news")
element2 = driver.find_element(by="id", value="blog-news")
```
* 说明  
当前ID没有重复值，所有可以直接用`find_element***`定位元素，如果ID存在重复则在运行的时候会找不到元素，此时需要使用`find_elements***`，假设`blog-news`存在重复值，则定位方式如下：
```python
element3 = driver.find_elements_by_id("blog-news")
element4 = driver.find_elements(by="id", value="blog-news")
```
使用`driver.find_element(by=by, value=value)`方式定位时，by传入的是定位方式，`by`在`selenium.webdriver.common.by.By`类中，各种定位方式对应关系如下：
```python
CLASS_NAME = 'class name'
CSS_SELECTOR = 'css selector'
ID = 'id'
LINK_TEXT = 'link text'
NAME = 'name'
PARTIAL_LINK_TEXT = 'partial link text'
TAG_NAME = 'tag name'
XPATH = 'xpath'
```

# Class定位
* 目标
查找含有`highlighter-rouge`类的元素
* 实现
```python
element1 = driver.find_element_by_class_name("highlighter-rouge")
element2 = driver.find_element(by="class name", value="highlighter-rouge")
```
* 说明  
当前`class name`没有重复值，所有可以直接用`find_element***`定位元素，如果`class`存在重复则在运行的时候会找不到元素，此时需要使用`find_elements***`，假设`highlighter-rouge`存在重复值，则定位方式如下：
```python
element3 = driver.find_elements_by_class_name("highlighter-rouge")
element4 = driver.find_elements(by="class name", value="highlighter-rouge")
```
另外`class`在实际项目中经常都是以组合的方式出现，但是`find_element_by_class_name()`只能是定位单各`class name`，复合`class name`的时候需要使用`css`定位方式

# Name定位
* 目标  
查找name值为top的元素
* 实现
```python
element1 = driver.find_element_by_name("top")
element2 = driver.find_element(by="name", value="top")
```
* 说明  
当前name没有重复值，所有可以直接用`find_element***`定位元素，如果`name`存在重复则在运行的时候会找不到元素，此时需要使用`find_elements***`，假设top存在重复值，则定位方式如下：
```python
element3 = driver.find_elements_by_class_name("top")
element4 = driver.find_elements(by="class name", value="top")
```

# 标签（tag name）定位
tag name即标签名称，如：a、input、button、img等

* 目标  
查找页面中的a标签  
* 实现
```python
element1 = driver. find_element_by_tag_name("a")
element2 = driver. find_element(by="tag name", value="a")
```
* 说明  
当前标签没有重复值，所有可以直接用`find_element***`定位元素，如果name存在重复则在运行的时候会找不到元素，此时需要使用`find_elements***`，假设a存在重复值，则定位方式如下：
```python
element3 = driver.find_elements_by_class_name("a")
element4 = driver.find_elements(by="class name", value="a")
```

# 超链接文本（Link text）定位
* 目标  
查找页面中的a标签
* 实现  
```python
element1 = driver. find_element_by_link_text("猜猜看")
element2 = driver. find_element(by="tag name", value="猜猜看")
```
* 说明  
当前标签没有重复值，所有可以直接用```find_element***```定位元素，如果name存在重复则在运行的时候会找不到元素，此时需要使用```find_elements***```，假设"猜猜看"存在重复值，则定位方式如下：
```python
element3 = driver.find_elements_by_class_name("猜猜看")
element4 = driver.find_elements(by="class name", value="猜猜看")
```
# 超链接模糊定位（partial link text）
* 目标  
查找页面中的a标签
* 实现  
```python
element1 = driver. find_element_by_link_text("猜猜看")
element2 = driver. find_element(by="tag name", value="猜猜看")
```
* 说明  
当前标签没有重复值，所有可以直接用```find_element***```定位元素，如果`name`存在重复则在运行的时候会找不到元素，此时需要使用```find_elements***```，假设"猜猜看"存在重复值，则定位方式如下：
```python
element3 = driver.find_elements_by_class_name("猜猜看")
element4 = driver.find_elements(by="class name", value="猜猜看")
```
# Xpath定位
## 选取节点
### 精确选择节点
XPath使用路径表达式在 XML 文档中选取节点。节点是通过沿着路径或者step来选取的  
#### 路径表达式
表达式 | 描述 |
:-: | :-: |
nodename | 选取此节点的所有子节点|
/ | 从根节点选取。
// | 从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。
. | 选取当前节点。
.. | 选取当前节点的父节点。
@ | 选取属性。

### 选取未知节点
XPath 通配符可用来选取未知的 XML 元素。  

通配符 | 描述|
:-: | :-: |
* | 匹配任何元素节点。|
@* | 匹配任何属性节点。|
node() | 匹配任何类型的节点。|

### 选取若干路径
通过在路径表达式中使用"|"运算符，您可以选取若干个路径。

## 绝对路径定位
绝对路径表示从html的根节点开始一层一层的往下查找元素，始于正斜杠（/）并且每层元素之间使用正斜杠（/）  

* 目标  
查找第一个a标签下的"猜猜看"
* 实现  
Xpath定位表达式
```html
/html/body/a[.="猜猜看"]
/html/body/a[text()="猜猜看"]
```
Python定位语句
```python
element1 = driver.find_element_by_xpath('/html/body/a[.="猜猜看"]')
element2 = driver.find_element_by_xpath('/html/body/a[text()="猜猜看"]')
```
* 说明  
使用绝对定位是十分不灵活的，一旦页面结构发生变化，原来的表达式就可能失效，需要重新维护，成本会增加。而且在实际项目中页面结构可能非常复杂，会造成xpath表达式非常长，不容易理解。所以不建议使用绝对定位。
## 相对路径定位
相对路径的每一步都根据当前节点集中的节点来进行计算，起始于双正斜杠（//）
* 目标    
查找第一个a标签下的"猜猜看"
*  实现  
Xpath表达式
```xpath
//a[.="猜猜看"]
//a[text()="猜猜看"]
```
Python表达式
```python
element1 = driver.find_element_by_xpath('//a[.="猜猜看"]')
element2 = driver.find_element_by_xpath('//a[text()="猜猜看"]')
```
* 说明  
相对路径xpath定位表达式简洁易读，而且不容易受页面结构变化的影响。使用时应尽量保证表达的简洁性。
## 索引定位
索引定位表示摸个被定位的页面元素在其父元素节点下的同名元素中的位置序号，起始序号为1

* 目标  
查询页面中的第二个div  
* 实现  
Xpath表达式
```xpath
//div[2]
```
Python表达式
```python
element = driver.find_element_by_xpath("//div[2]")
```
## 属性定位
### 精确属性定位
* 目标  
选择alt值等于"点我试试呀"的img元素  
* 实现  
Xpath表达式  
```xpath
//img[@alt="点我试试呀"]
```
Python表达式  
```python
element = driver.find_element_by_xpath('//img[@alt="点我试试呀"]')
```
### 模糊属性定位
模糊定位的函数有如下三个：`starts-with (str1,st2), contains (str1,str2),text()`

* 目标  
查找alt属性值包含"点我"的元素  
* 实现  
Xpath表达式  
```xpath
//img[starts-with(@alt,"点我")
//img[contains(@alt,"点我")
```
Python表达式
```python
element1 = driver.find_element_by_xpath('//img[starts-with(@alt,"点我")')
element2 = driver.find_element_by_xpath('//img[contains(@alt,"点我")')
```

## 轴定位
 
Xpath轴关键字 | 轴的定义说明 | 定位表达式实例 | 表达式解释 |
:-: | :-: | :-: | :-: |
parent | 选取当前节点的父节点 | //img[@alt='div2-img2']/parent::div | 查找到alt属性为div2-img2的img元素，并基于图片找到其上一级的div元素 |
child | 选取当前节点的子节点 | //div[@id='div1']/child::img | 查找id为div1的div标签，基于当前div查找标签为img的子节点 |
ancestor | 选取当前节点的所有上层节点 | //img[@alt='div2-img2']/ancestor::div | 查找alt属性为div2-img2的图片，基于当前图片找到其上级的div页面元素 |
descendant | 选取当前节点所有下层节点 | //div[@id='div2']/descendant::img | 查找id属性为div2的div元素，在查找其下级所有节点中的img元素 |
following | 选取当前节点之后显示的所有节点 | //div[@id='div1']/following::img | 查找到ID属性为div1的div元素，并基于div的位置找到它后面节点中的img元素 |
following-sibling | 选取当前节点所有的平级节点 | //img[@alt='div1-img1']/following-sibling::input | 查找到alt属性为div1-img1的img页面元素，并基于img的位置找到后续节点中的input元素 |
preceding | 选取当前节点前面所有的节点 | //img[@alt='div2-img2']/preceding::div | 查找到alt属性为div2-img2的图片页面元素，并基于图片的位置找到它前面节点中的div元素 |
preceding-sibling | 选取当前节点前面所有平级的节点 | //img[@alt='div2-img2']/preceding-sibling::a[1] | 查找到alt属性值为div2-img2的图片元素，基于图片位置找到它前面同级节点的第二个链接页面元素 |
ancestor-or-self | 选取当前节点的所有先辈（父、祖父等）以及当前节点本身。 | | |	　
attribute | 选取当前节点的所有属性	 | | |　
namespace | 选取当前节点的所有命名空间节点。 | | |	　
self |  选取当前节点。 | | |

## 文本定位
text()函数可以定位到元素文本包含某些关键内容的页面元素  
```
//p[text()=" openstf项目开源地址："]
//p[.=" openstf项目开源地址："]
//p[contains(text(),"openstf")]
//p[contains(.,"openstf")]
```
python表达式
```python
Driver.find_element_by_xpath('//img[contains(@alt,"点我")')
```

# CSS定位
## 绝对路径定位
* 目标
查找第一个文本为"猜猜看"的a标签
* 实现
CSS表达式
```
html>body>div>a[.="猜猜看"]
```

python表达式
```python
driver.find_element_by_css_selector('html>body>div>a[.="猜猜看"]')
```


## 相对路径定位
* 目标  
查找第一个文本为"猜猜看"的a标签  
* 实现  
CSS表达式  
```
a[.="猜猜看"]
```

Python表达式
```python
driver.find_element_by_css_selector('a[.="猜猜看"]')
```
## 类名定位
* 目标
查找第一个类名为"blogpost-body"的div元素
* 实现
CSS表达式
```html
div. blogpost-body
```
python表达式
```python
driver.find_element_by_css_selector("div. blogpost-body")
```
* 说明
对于复合class，如`<input class="btn btn-lg btn-default" type="text">`，直接写上所有的class即可，即：`driver.find_element_by_css_selector("input. btn.btn-lg.btn-default")`
标签名不是必须的

## 属性定位
### ID属性定位
* 目标  
查找页面中第一个id为"cnblogs_post_body"div元素  
* 实现  
CSS表达式  
```html
div# cnblogs_post_body
```
Python表达式
```python
driver.find_element_by_css_selector("div# cnblogs_post_body")
```

### 其他属性定位
其他属性是指除id、class以外的所有属性，如img的src、alt属性，input的type、placeholder等
* 目标  
查找页面中alt属性等于"点我试试呀"的img元素  
* 实现  
CSS表达式  
```css
img[alt="点我试试呀"]
```
Python表达式
```python
driver.find_element_by_css_selector('img[alt="点我试试呀"]')
```
* 说明  
如果单独依靠某个属性无法唯一定位元素，则可以写多个属性，如下：
```css
img[alt="点我试试呀"][src="/images/bg.jpg"]
```
```python
driver.find_element_by_css_selector('img[alt="点我试试呀"] [src="/images/bg.jpg"]')
```

### 模糊属性定位
模糊属性定位经常使用的三个正则表达式`^、$、*`
* 目标  
查找链接地址是"http://www.baidu.com"的a标签  
* 实现  
CSS表达式  
```css
a[href^="http://www.baidu"]
a[href$="baidu.com"]
a[href*="baidu"]
```

python表达式
```python
find_element_by_css_selector('a[href^="http://www.baidu"]')
find_element_by_css_selector('a[href^=" a[href$="baidu.com"]')
find_element_by_css_selector('a[href*="baidu"]')
```
## 子页面元素查找
* 目标
查找id为home的div下的class为highlighter-rouge的div
* 实现
CSS表达式
```css
div#home>div.highlighter-rouge
```
python表达式
```python
driver.find_element_by_css_selector("div#home>div.highlighter-rouge")
```
## 伪类定位
* 目标  
查找`div#home`下的第一个子元素  
* 实现
CSS表达式
```css
div#home :first-child
```
python表达式
```python
dirver.find_element_by_css_selector("div#home :first-child")
```
更多伪类见附录[CSS伪类](/addition/css/)
