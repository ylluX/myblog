# hexo+netX主题搭建简易博客

## 工具安装
Hexo 可以说是目前最流行的博客框架了，基于Nodejs，它依赖Git, Nodejs等工具.
1. 安装git
2. [安装nodejs](http://nodejs.cn/download/)
3. 安装hexo: ```npm install hexo-cli -g```

## 创建仓库
1. 注册github账号, 注意认真填写username, 今后你的域名将会是: username.github.io
2. 创建仓库, 仓库名为: usearname.github.io, 完整地址为: https://github.com/username/username.github.io (注意username)

## 创建博客
1. 创建myblog站点: ```hexo init myblog```
2. 进入工作目录: ```cd myblog```
3. 安装发布工具: ```npm install hexo-deployer-git --save```
3. 下载[netX](https://github.com/iissnan/hexo-theme-next)主题: ```git clone --branch v5.1.2 https://github.com/iissnan/hexo-theme-next themes/next```
4. 站点基础配置: 
    ```
    title: ylluX博客 # 设置站点名字
    author: ylluX # 设置站点作者
    language: zh-Hans # 设置中文
    theme: next # 设置主题
    deploy:
        type: git # 使用Git发布
        repo: https://github.com/ylluX/ylluX.github.io.git # 设置站点的远程仓库
    ```
5. [主题配置](http://theme-next.iissnan.com/getting-started.html)

## 写作,测试和发布
1. 写作: 在myblog/source/_posts下写博客吧(makedown, html等)
2. 测试: ```hexo server```启动测试服务, 然后访问:https://localhost:4000
3. 发布: ```hexo clean```, ```hexo generate```, ```hexo deploy``` (以后更新发布, 就使用这三条命令)


## 在另一台电脑上更新blog

该仓库中缺少node_modules文件夹(被.gitignore忽略).

如果在其它电脑上更新blog, 可以:

```
# 克隆项目
git clone git@github.com:ylluX/myblog.git
# hexo 初始化一个临时文件(为了获得node_modules)
hexo init temp
# 将temp/node_modules复制到myblog
cp temp/node_modules myblog
# 删除temp
rm -r temp
# 进入myblog项目
cd myblog
# 安装hexo-deployer-git自动部署发布工具 
npm install hexo-deployer-git --save
# 因为网站使用了local search的站内搜索功能,所以需要安装相应工具
npm install hexo-generator-searchdb
```

然后写作 ,更新, 发布即可

## 参考
1. [5分钟 搭建免费个人博客](http://www.jianshu.com/p/4eaddcbe4d12)
2. [NexT](http://theme-next.iissnan.com/getting-started.html)
3. [使用Hexo搭建博客（三），博客配置、主题和写作](http://www.jianshu.com/p/db7e64d86067)