## 基于hexo的个人博客搭建过程
测试站点：www.sdwangblog.top

本博客使用 Github Page + Hexo 搭建的，主题采用的是[yilia](https://github.com/litten/hexo-theme-yilia) ，在此感谢作者[litten](https://github.com/litten)。

以下为个人参照教程在Mac上的搭建的过程总结，以及中途“小插曲”记录，希望对大家能有帮助。
### 准备工作
hexo是一款基于Node.js的静态博客框架，所以需要安装些必须的配置环境；
- 安装Node.js（个人采用了源码编译安装）；
```
$ wget http://nodejs.org/dist/v0.10.17/node-v8.4.0.tar.gz
$ tar xvf node-v8.4.0.tar.gz
$ cd node-v8.4.0
$ ./configure
#该编译过程耗时大概20分钟
$ make
$ make install
#查看当前安装的Node版本
$ node -v
$ npm -v
#由于国内访问npm官方镜像经常出问题，可通过配置淘宝NPM镜像，用cnpm代替默认的npm。
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```
其间因本地没有安装Xcode执行./configure时我遇到了问题：
```
1.Install Xcode (get it from https://developer.apple.com/xcode/) if you don't have it yet.
2.Ensure Xcode app is in the /Applications directory (NOT /Users/{user}/Applications).
  Xcode: /Applications/Xcode.app/Contents/Developer
3.sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```
- 安装了git客户端，Mac自带；
- 用github账号创建一个仓库，比如你的github用户名为test,那么就新建 test.github.io 的仓库。
- 绑定域名，默认可以用test.github.io访问，如果你想更个性一点，绑定一个自己的域名，当然也是OK的。

### 使用hexo写博客
#### 安装hexo：
```
$ cnpm install -g hexo-cli
$ cnpm install hexo --save
#验证hexo安装是否正确
$ hexo -v
```
#### 使用hexo
```
$ cd ~/Workspaces/hexo/
$ hexo init

#生成静态页面
$ hexo g
#开启本地预览服务，http://localhost:4000 即可看到内容
$ hexo s
```
静态页面会生成在public文件夹中，仅这些文件将会被提交到GitHub。
### 修改主题
默认主题比较丑，个人换成了hexo-theme-yilia这个主题：
```
#下载yilia主题
$ cd ~/Workspaces/hexo/
$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
修改_config.yml中的theme: landscape改为theme: yilia，然后重新执行hexo g来重新生成。
```
如果出现一些莫名其妙的问题，可以先执行hexo clean来清理一下public的内容，然后再来重新生成和发布。
### 上传之前
```
$ git config --global user.name "你的用户名"
$ git config --global user.email "你的邮箱"
$ git config --global user.passwork "你的密码"
#安装hexo git插件
$ cnpm install hexo-deployer-git --save
#配置`_config.yml`中有关deploy的部分
deploy:
    type: git
    repository: git@github.com:xxx/xxx.github.io.git
    branch: master
```    
⚠️：从hexo提交代码时会把以前的所有代码都删掉，保险起见，建议本地先clone一份。

### 上传到GitHub
$ hexo d会将本次所有改动的代码提交，没有改动的不会；

### 保留CNAME、README.md等文件
提交之后网页上一看，发现以前其它代码都没了，此时不要慌，一些非md文件【CNAME、README.md】可以把他们放到source文件夹下，这里的所有文件都会原样复制（除了md文件）到public目录的；

由于hexo默认会把所有md文件都转换成html，包括README.md，所有需要每次生成之后、上传之前，手动将README.md复制到public目录，并删除README.html。

### 关于 Fork 和 Star
如果觉得我的博客文章还不错的话，欢迎点个 star 。谢谢！
