#蹒跚学步 我的nodejs

##初识nodejs
-2015-04-25驱车从北京来天津   

	我的第一天   

-OSX下的安装    

	node -v 在安装成功后可查看版本号   

-git初识   

	mkdir XXX   

	cd XXX   

	git init 初始化   

	git add -A   

	git commit -m "first commit"   

	git remote add origin https://github.com/meng1h/demo1.git 只在第一次用到此处的origin对应下面push的origin   

	git push -u origin master 这里的master是分支   

##express
	sudo npm install -g express-generator 全局安装    
	express -t jade nodejs-1 创建项目   
	
## mongoose
	在实例上暴露出的所有常见操作有   
	find,findOne,remove,update,count

## req..服务端处理的区别  
	get /article ? limit=10 req.query.limit   
	get /article / :article_id req.params.article_id   
	post /article {json} req.body.article

## 服务器各层
	route->middle->controler->service->DAO->model  

## 基础知识ppt
	http://nodeonly.com/nodesang/#/5

##html 语法   
	用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
	嵌套元素应当缩进一次（即两个空格）。
	对于属性的定义，确保全部使用双引号，绝不要使用单引号。
	不要在自闭合（self-closing）元素的尾部添加斜线 （例如<img src="images/company-logo.png" alt="Company">）
	不要省略可选的结束标签（closing tag）（例如，</li> 或 </body>）。

## 问题
	为什么用两个空格代替制表符，能够保持在所有环境下的展现一致性

	