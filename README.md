# 个人博客搭建 #

## 准备工作 ##

安装必备的工具软件：

- 具体可参照[Hexo官网](https://hexo.io/zh-cn/docs/index.html)

	1. 安装[Git工具](https://git-scm.com/)，安装[Node.js](https://nodejs.org/en/)

	2. 注册[GitHub账号](https://github.com/)，注册[Coding账号](https://coding.net/)

	3. 安装写博客工具[MarkDownPad2](http://markdownpad.com/)（个人选择）
	
		- 注册邮箱：Soar360@live.com
		- 授权秘钥：[授权码](http://cazaea.com/markdownkey.html "点击获取")

		- *下载[Awesomium 1.6.6 SDK](http://markdownpad.com/download/awesomium_v1.6.6_sdk_win.exe)解决MarkdownPad2在win10下报HTML 渲染错误(This view has crashed)*

<!--more-->

## 建站正式开始 ##

以上必备应用程序安装完成后(桌面右击打开Git Bash Here)

![点击Git Bash Here](https://i.imgur.com/4pqaVRh.png)

![打开后画面](https://i.imgur.com/Wlsllc5.png)

输入`npm install -g hexo-cli`，使用npm安装Hexo，安装成功如下：

![安装Hexo成功](https://i.imgur.com/J5aeujt.png)

安装成功后执行下面命令`hexo -v`，信息如下：

![版本信息](https://i.imgur.com/uWtiiks.png)

接着执行下面命令`hexo init Cazaea`，初始化自己的博客文件夹，运行后，会在桌面生成一个Cazaea文件夹。

- 我这里使用了Cazaea文件夹，你可以随便命名一个自己喜欢的文件夹，当然，你也可以先输入`cd d:/`，再输入`hexo init Cazaea`命令，在D盘下生成文件夹Cazaea

![初始化成功](https://i.imgur.com/PY3LNNA.png)

![桌面生成文件夹](https://i.imgur.com/uy2n70Z.png)

文件夹内容：

![文件夹内容展示](https://i.imgur.com/KaySXLH.png)

通过执行代码`cd Cazaea`进入刚刚创建的文件夹，执行`hexo s`开启本地服务

![开启本地服务](https://i.imgur.com/JJKwx23.png)

打开浏览器，输入 ***http://localhost:4000/*** 预览最原始页面

![初始页面](https://i.imgur.com/pqxBavC.png)

此时，本地已没有问题，接下来就是要把它部署到远程服务器了。

## 建立GitHub Pages ##
这时候就要用上之前准备的账号了，登录GitHub，选择新建仓库

![新建仓库](https://i.imgur.com/S6Ixb89.png)

这个仓库比较特殊，它要按照如下格式进行命名：你的GitHub用户名.github.io。

![创建仓库](https://i.imgur.com/NeJd25T.png)

新建好这个仓库后，点击右上角Settings

![新建仓库参考](https://i.imgur.com/dkvyJgD.png)

然后点击settings选项，向下翻到Git Pages选项

![选择主题](https://i.imgur.com/fx8hfS6.png)

点击`Choose the theme`选择一个主题，接下来， 你会看到

![Git网站走通](https://i.imgur.com/ulhQxPk.png)

### 配置SSH公钥 ###

配置Github的SSH密钥可以让本地git项目与远程的github建立联系，让我们在本地写了代码之后直接通过git操作就可以实现本地代码库与Github代码库同步。操作如下：

1.看看是否存在SSH密钥(keys)
首先，我们需要看看是否看看本机是否存在SSH keys,打开Git Bash,并运行:

    cd ~/. ssh

- 检查你本机用户home目录下是否存在.ssh目录
如果，不存在此目录，则进行第二步操作，否则，你本机已经存在ssh公钥和私钥，可以略过第二步，直接进入第三步操作。

2.创建一对新的SSH密钥(keys)，这将按照你提供的邮箱地址，创建一对密钥

    $ssh-keygen -t rsa -C "your_email@example.com" 


- 接着，根据提示，你需要输入密码和确认密码,在这里我们直接enter，不用输入密码。
	 
	    Enter passphrase (empty for no passphrase): [Type a passphrase]
		Enter same passphrase again: [Type passphrase again]

- 输入完成之后，屏幕会显示如下信息：

    	Your identification has been saved in /c/Users/you/.ssh/id_rsa.Your public key 
		has been saved in /c/Users/you/.ssh/id_rsa.pub.The key fingerprint 
		is:01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com

3.在GitHub账户中添加你的公钥

- 运行如下命令，将公钥的内容复制到系统粘贴板(clipboard)中。

    	clip < ~/.ssh/id_rsa.pub

- 接着：
登陆GitHub,进入你的Account Settings.

![添加Key](https://i.imgur.com/486kQ9A.png)

4.测试

- 可以输入下面的命令，看看设置是否成功，git@github.com的部分不要修改：
- 成功后你会看到

		 Hi Cazaea! You've successfully authenticated, but GitHub does not provide shell access.

5.设置用户信息

    git config --global user.name "Cazaea"//用户名
	git config --global user.email "wistorm@mail.com"//填写自己的邮箱

### 为GitHub Pages配置部署信息 ###

打开之前生成的文件夹，找到`_config.yml`文件，为GitHub Pages配置站点文件

![为Git配置站点文件](https://i.imgur.com/xt7GIpF.png)

然后在命令窗口执行下面命令,安装相关部署插件

    npm install hexo-deployer-git --save

安装完成后，执行

    hexo g
	hexo d

此时会让你输入GitHub的账号和密码，输入后在浏览器中输入 ***https://Cazaea.github.io/***  应该就可以访问了,如果未显示，稍等一下，再进行访问，GitHub部署需要一点时间。

## 配置Coding Pages ##
为了一丝一毫的响应速度，推荐同时配置Coding Pages，使网站可以国内请求Coding，海外请求GitHub。从此，你的网站不只快了一点点。

Coding Pages配置与GitHub Pages配置步骤类似，照着同样的步骤就可以搞定。

★ 其中有一个坑，勿跳：

- 当你创建项目后，无法建立分支（Coding提示：代码未上传，请先上传代码）。此时，你可以先通过配置`_config.yml`文件，将代码上传

		deploy:
		- type: git
		  repository: https://github.com/Cazaea/Cazaea.github.io.git
		  branch: master

		# 在之前配置的GitHub Pages之后添加Coding Pages配置

		- type: git
		  repository: https://git.coding.net/Cazaea/Cazaea.git
		  branch: coding-pages

然后在Coding.net中打开自己创建的项目，添加分支master：

复制Commit id
![](https://i.imgur.com/t9NOIAY.png)

粘贴Commit id，完成master分支创建
![](https://i.imgur.com/xVlIuSP.png)

创建完成，将coding-pages分支删除，再将_config.yml文件更改为：

    deploy:
		- type: git
		  repository: https://github.com/Cazaea/Cazaea.github.io.git
		  branch: master

		# 在之前配置的GitHub Pages之后添加Coding Pages配置

		- type: git
		  repository: https://git.coding.net/Cazaea/Cazaea.git
		  branch: master

## 更换主题 ##

首先去[hexo皮肤网站](https://hexo.io/themes/),选择一款进入它的GitHub地址然后将clone的文件移动到themes文件夹下。然后修改`_config.yml`文件中的`theme`为你所选择的主题的名称即可。

推荐使用next主题，执行代码：

    git clone https://github.com/iissnan/hexo-theme-next themes/next

修改站点配置文件`_config.yml`，找到以下部分：

	# Extensions
	## Plugins: http://hexo.io/plugins/
	## Themes: http://hexo.io/themes/
	theme: landscape

修改为

    # Extensions
	## Plugins: http://hexo.io/plugins/
	## Themes: http://hexo.io/themes/
	# theme: landscape
	theme: next

然后执行：

    hexo g -d

★ 传送门必看：修改主题配置信息，请参照[Zhiho's Blog](https://zhiho.github.io/2015/09/29/hexo-next/)

## 域名绑定 ##

关于购买域名，此处不再赘述，说的太多，容易跑题。

之前已经写好了GitHub Pages和Coding Pages服务，只是可以通过[https://Cazaea.github.io](https://Cazaea.github.io)和[http://Cazaea.coding.me](http://Cazaea.coding.me)访问，跟自己的域名一毛钱关系没有，下面，就开始让他们有关系。

1. 在文件夹Cazaea下的source文件夹创建文件CNAME，无后缀名。
2. 打开文件（我用的PS Pad），写入文本（自己的域名，切记，**不带http://www，例如：cazaea.com**）

![域名文件](https://i.imgur.com/Hsi65a8.png)

运行

    hexo g -d

将文件提交至GitHub和Coding，此时你的域名仍然不能访问，不要着急，你只是缺少了域名的解析。

之前百度很多，域名解析试了很多，很多能实现[cazaea.com](http://cazaea.com)访问，不能实现[www.cazaea.com](http://www.cazaea.com)的访问。

★最终通过摸索，完成了域名的解析，域名最终都能访问。具体如下：

![域名解析](https://i.imgur.com/sPX5Qjb.png)

## 加入搜索引擎 ##

由于加入Google，需要翻墙，具体翻墙工具个人选择，推荐Shadowsocks，Lantern

★ 切记：如果使用推荐的下载`[googleff0226f76d5f451b.html, baidu_verify_vHC5EAW09E.html]`形式，请将下载好的文件放进Cazaea\source文件夹，并且编辑此.html文件，添加标题，如下：


- Google html文件

		layout: false
		sitemap: false
		---
		google-site-verification: oogleff0226f76d5f451b.html

- Baidu html文件

    	layout: false
		sitemap: false
		---
		vHC5EAW09E

★ 传送门：

- 参考①:[HarleyWang's Blog](https://github.com/HarleyWang93/blog/issues/26)
- 参考②:[JI's Blog](http://www.yuan-ji.me/Hexo-%E4%BC%98%E5%8C%96%EF%BC%9A%E6%8F%90%E4%BA%A4sitemap%E5%8F%8A%E8%A7%A3%E5%86%B3%E7%99%BE%E5%BA%A6%E7%88%AC%E8%99%AB%E6%8A%93%E5%8F%96-GitHub-Pages-%E9%97%AE%E9%A2%98/)

## 配置文件（最关键） ##

这一步操作，网上的参照碰到了太多的坑，时间太久，很多Hexo建站博客都不够完善，且错误较多。
下面，具体说明：

- 首先是配置`_comfig.yml`站点文件
(这是我最完整的配置，仅做参考，切记每个冒号后都有空格)

		# Hexo Configuration
		## Docs: https://hexo.io/docs/configuration.html
		## Source: https://github.com/hexojs/hexo/
	
		# Site #博客的基本信息
		title: Cazaea's Blog # 博客标题
		subtitle: 一直相信：越努力，越幸运；越沟通，越亲近。 # 博客副标题
		description: 小有文艺的攻城狮 # 博客描述，部分主题会用来生成简介
		author: YourName # 博客作者
		language: zh-Hans # 语言
		timezone:
		
		# URL
		## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
		url: http://yoursite.com # 你自己的域名
		root: / # 根目录位置，如果只是github pages的子目录需要更改
		permalink: :year/:month/:day/:title/ #:title-:year/:month/:day/
		permalink_defaults:
		
		# Directory #文件结构 默认即可
		source_dir: source
		public_dir: public
		tag_dir: tags
		archive_dir: archives
		category_dir: categories
		code_dir: downloads/code
		i18n_dir: :lang
		skip_render:
		
		# Writing
		new_post_name: :title.md # File name of new posts
		default_layout: post
		titlecase: false # Transform title into titlecase
		external_link: true # Open external links in new tab
		filename_case: 0
		render_drafts: false
		post_asset_folder: false
		relative_link: false
		future: true
		highlight: # 代码高亮
		enable: true # 是否启用
		line_number: true # 是否显示行号
		auto_detect: false
		tab_replace:
  	
		# Home page setting
		# path: Root path for your blogs index page. (default = '')
		# per_page: Posts displayed per page. (0 = disable pagination)
		# order_by: Posts order. (Order by date descending by default)
		index_generator:
		  path: ''
		  per_page: 3 # 首頁默认10篇文章标题 如果值为0不分页
		  order_by: -date
  		
		archive_generator: # 归档页面
	  	per_page: 10 # 默认10篇文章标题
	  	yearly: true  # 生成年视图
	  	monthly: true # 生成月视图
	  
		tag_generator: # 标签分类页面
	  	per_page: 10 # 默认10篇文章
	  	
		category_generator: # 分类页面
	  	per_page: 10 # 默认10篇文章
	  	
		# Category & Tag # 分类与标签
		default_category: uncategorized
		category_map:
		tag_map:
	
		# Date / Time format # 日期显示格式
		## Hexo uses Moment.js to parse and display date
		## You can customize the date format as defined in
		## http://momentjs.com/docs/#/displaying/format/
		date_format: YYYY-MM-DD
		time_format: HH:mm:ss
		
		# Pagination # 分页器
		## Set per_page to 0 to disable pagination
		per_page: 6
		pagination_dir: page
	
		# Extensions # 拓展
		## Plugins: https://hexo.io/plugins/
	
		# 自动生成sitemap
		sitemap:
	 	path: sitemap.xml
	 	
		baidusitemap:
	 	path: baidusitemap.xml
		
		## Themes: https://hexo.io/themes/
		# 主题更换
		theme: next
	
		# Deployment # 部署参数
		## Docs: https://hexo.io/docs/deployment.html
		deploy:
	 	- type: git
	  	  repository: https://github.com/yourgitname/yourgitname.github.io.git # (这里复制你自己的Git项目地址)
	  	  branch: master
		  
	 	- type: git
	  	  repository: https://git.coding.net/yourcodingname/yourcodingname.git # (这里复制你自己的Coding项目地址)
	  	  branch: master
	
- 其次，主题配置文件，同样名为`_config.yml`，位于主题文件夹下，`Cazaea\themes\next`。

		# 主题样式修改
    	# Schemes
		scheme: Mist  # 去掉默认的注释即可切换为Mist主题
		#scheme: Mist
		#scheme: Pisces
		#scheme: Gemini

	在`Cazaea\themes\next\source\images`文件夹下放入自己的头像。

		# 修改头像
		avatar: /images/head.jpg

	- 具体请参照：

		修改主题配置信息，请参照[Zhiho's Blog](https://zhiho.github.io/2015/09/29/hexo-next/)

		整体配置信息，请参照[HarleyWang's Blog](https://github.com/HarleyWang93/blog/issues/26)

★ 个性化设置：

- Next主题个性化：[Moorez](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)
- 添加音乐：[LeviDing](http://www.dingxuewen.com/2017/03/11/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E7%9A%84%E4%B8%AA%E6%80%A7%E5%8C%96%E8%AE%BE%E7%BD%AE%E4%B8%89/)
- 热度调试：[WangHao](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)

★ 特殊说明：	

- GitHub Pages对自定义域名支持HTTPS：[Cafeting](https://likfe.com/2018/05/03/github-pages-custom-domains-support-https/)
	
		- 切记：在项目主配置文件_config.yml中也要讲域名信息更改为https://yoursite.com

- 域名解析GitHub IP地址更换：

	    - 185.199.108.153
    	- 185.199.109.153
    	- 185.199.110.153
    	- 185.199.111.153

## 最后 ##

搭建博客，来来回回费了不少的功夫。当然，我也是一个又一个的坑踩过来的。在这期间，我阅读了很多相关的博文，也学习了不少的东西，在此向相关博文的作者表示感谢，谢谢你们的文章让我进步。

时代在进步，技术在更新。当前这篇Hexo搭建博客的文章，可能随着时间的推移，又会有新的坑出现。各位放心，一定及时更新。
