# Rails Girls App
详细介绍请见[这篇文档](http://guides.railsgirls.com/app/)

## 第一步：建立一个rails应用
### 目标
建立一个rails项目，并成功在浏览器中打开它的欢迎页面。

### 命令解析
`mkdir`是建立一个文件夹，后面跟一个字符串当文件夹名

`cd`是进入某一个文件夹中，可以用相对路径，也可以用绝对路径

`pwd`可以查看当前目录的绝对路径

`rails new`命令可以帮助你快速建立一个rails项目

`rails server`用来启动当前目录下的rails项目

### 这一步所需操作
```
mkdir projects
cd projects
rails new railsgirls
cd railsgirls
rails server
```
完成这些步骤后，注意看命令行的提示信息，访问打印出来的URL就可以打开你的第一个rails应用啦

## 第二步：用脚手架快速搭建应用
不行了。。这种正经的文档写起来太枯燥，而且刚才发现了另一个非常简单的[单步演示](https://github.com/lbain/railsgirls)，虽然是英文版，但相信以大家的水平都是能看懂的（说真的看不懂的那些自己查词典去→_→）
下面我决定用生（dou）动（bi）一点的语言来讲解剩余的步骤。
## 真·第二步
### 目标
大家都有脑洞大开的时候吧？为了能让你偶尔突变一次的脑细胞不被浪费，现在你想把这些灵光一闪的Idea都记录下来，并且可以在自己的这个rails站点上查询、修改、删除它。

(事实上，这个目标也是我从脑洞中提取出来的:joy: 真实目标请参看英文原文)

### 步骤

首先，在项目的根目录下执行命令：

```
rails generate scaffold idea name:string description:text picture:string
```
其次，更新数据库+启动server。一组具备增删改查功能的基本页面就这样完成啦！

是不是想问“啊？这就完了？”

对的，就这么简单，现在打开`0.0.0.0:3000/ideas`，去试用一下你刚创建的功能吧~

### 详细解(tu)析(cao)
看到`scaffold`这个东西的时候，相信大家的第一反应应该都差不多：这是什么鬼?:frowning:

第一步中的rails new还好说，毕竟很多语言建立工程项目时都有类似的便捷方式。但这个译作`脚手架`的东东，怎么一行命令就把router、controller、view、model & migration的代码全写好了，甚至连测试都补全了，它这么棒还要我们干嘛。。

事实上呢，个人认为scaffold并没有太大的用途，它更适合让初学者来熟悉rails创建和使用对象的基本流程，而一旦掌握了这部分内容，scaffold创建的一堆冗余文件反而会有点过犹不及的感觉。倒是generate其它东西命令会更常用一些，它可以根据模板快速创建指定的基本文件，能节省很多时间。

另一个值得一提的是路由的配置，打开`config/routes.rb`文件，可以看到真正起作用的只有一行代码`resources :ideas`，但是它的存在却让我们可以同时访问四个页面，让Server识别7种请求，这是怎么做到的呢？

在回答这个问题之前，想先问一下小伙伴们知道CRUD吗？如果不清楚，那“增删改查”应该都知道吧。这是四种常用的跟数据对象打交道的方式，它也跟最常用的四种HTTP请求一一对应。

| 简写 | 全称 | 操作 | HTTP请求 |
| ------- | ------- | ------- | ------- |
| C | Create | 增 | POST |
| R | Retrieve | 查 | GET |
| U | Update | 改 | PUT |
| D | Delete | 删 | DELETE |

Rails的一大特点是开发速度快，不论是rails自身还是跟它集成的Gem，都在努力地做着同一件事：把常见的需求做成现成的轮子供大家使用。所以很多简单的RoR应用都只需要把各种轮子拿来拼接到一起即可成型。

`resources :ideas`也是这种便捷实现的一个体现，它将最常见的CRUD操作以及所需页面的routes集成到了一起，用一行代码实现了以下七个动作：（从而达到了偷懒的目的:joy:）

| HTTP动作 | 路径 | action |
| ------- | ------- | ------- |
| GET | /ideas  | index |
| GET | /ideas/new | new |
| POST | /ideas | create | 
| GET | /ideas/:id | show |
| GET | /ideas/:id/edit | edit |
| PUT | /ideas/:id | update |
| DELETE | /ideas/:id | delete |

## 第三步
### 目标
爱美是每个女孩儿的天性，那么你肯定无法容忍现在这么丑的页面，这一步我们就是要对网页的样式做些改变，让页面变得美美哒~

### 步骤
基本都是复制粘贴，所以直接参看教程吧：<http://guides.railsgirls.com/app/#design>

### 说明
HTML与CSS的关系，就像语法中的“主谓宾”和“定状补”的关系一样。

HTML是主谓宾，它自己就可以表达出完整的意思，但是并不生动。i.e. HTML可以组成完整的页面，但是并不美观。

CSS是定状补，它单独存在时并没有什么卵用，但是如果跟主谓宾(HTML)结合起来使用的话，就会让页面变得生动起来。

### 参考资料
* 这一步用到了[bootstrap](http://www.bootcss.com/)，推荐一个快速学习其布局的站点[Layout It](http://www.layoutit.com/)
* [W3School](http://www.w3school.com.cn/html/html_intro.asp)上可以查到很多HTML/CSS的详细说明，且大多配有相应的例子
* [三周三页面](http://juntao.gitbooks.io/3-web-designs-in-3-weeks/)也是快速学习HTML/CSS的一个有效途径（给邱大师打了个广告:smile:）


## 第四步
### 目标
丰富表单，增加图片上传功能，同时将已上传的图片显示在展示页面上。

### 步骤
还记得第二步中提到的便捷实现吗？既然图片上传也是常用功能之一，那自然也有相应的快(tōu)捷(lǎn)方法啦。

1.在Gemfile中为项目添加一个新的Gem：

```
gem 'carrierwave'
```
2.用命令`bundle install`下载并安装这个新添加的Gem

3.装是装好了，但是怎么用呢？这时候轮到[RubyGems](https://rubygems.org/gems/carrierwave)出场了。里面不但可以看到这个Gem的下载人数和历史版本，还能找到一系列的相关链接，其中就包括了[使用说明](http://www.rubydoc.info/gems/carrierwave/0.10.0)。

4.按照说明的提示，现在我们该使用`generate`来创建uploader了。在命令行里键入`rails g uploader picture`

> 这里的`g`是`generate`的缩写，同样的，`rails server`也可以简写成`rails s`

> 还有一个常用工具`rails console`，也可以简写成`rails c`

5.接下来就要把刚创建的uploader和Idea对象中的picutre属性绑定起来啦。在文件`app/models/idea.rb`中添加如下语句：

```
mount_uploader :picture, PictureUploader
```

6.将`app/views/ideas/_form.html.erb`文件中picture字段的属性改为文件：

```
<%= f.file_field :picture %>
```
到这里，文件上传功能就实现好了，如果启动server创建一个新Idea的话，就会发现上传的文件已经存储到PictureUploader配置的路径下了。但光传上去不行啊，我们还需要能直接在页面上看到，所以还需要最后一步：

7.打开文件`app/views/ideas/show.html.erb`与`index.html.erb`，将

```
<%= @idea.picture %>
```
更改为

```
<%= image_tag(@idea.picture.url, :size => "350x350") if @idea.picture.present? %>
```

好啦，第四步到此结束。现在我们的站点既能上传图片又能将它们显示在index与show这两个页面上了。


## 第五步
### 了解route相关知识
通过`rails server`可以访问两类文件：

* 一是直接放置在public目录下的静态文件。比如自动生成的404/500等页面，直接通过`/400.html`即可访问。
* 二是经过 route->controller->view 这样一个流程，最终返回的页面。前面看到的`/ideas`页面就属于这类。

要想知道router都可以处理哪些请求，可以通过命令`rake routes`来查看。通过修改`config/route.rb`文件，也可以自定义请求与controller之间的映射关系。

例如，若想把ideas的index页面作为首页，则可以添加如下路由规则：
```
root to: 'ideas#index'
```
当然，也可以通过把首页重定向到'/ideas'来实现同样的功能：
```
root to: redirect('/ideas')
```

更多的说明请参考RoR的[手册](http://guides.rubyonrails.org/routing.html)。
