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

###步骤

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

事实上呢，个人认为scaffold并没有太大的用途，它更适合让初学者来熟悉rails创建和使用对象的基本流程，而一旦掌握了这部分内容，scaffold创建的一堆冗余文件反而会有点过犹不及的感觉。倒是generate这个命令会更常用一些，它可以根据模板快速创建指定的基本文件，能节省很多时间。

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

