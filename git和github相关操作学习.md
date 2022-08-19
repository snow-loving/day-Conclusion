mac上传github文件相关操作
mac上传github项目文件相关指南

git remote -v  #查看当前链接
git remote remove origin #移除当间链接

一。准备工作

1注册github账号

2.安装git https://desktop.github.com git --verison

3.准备项目，将自己的文件放到任一一个位置

二。使用git命令操作

1打开终端，定位到项目文件夹

2配置ssh

cd ～/.ssh
#如果出现没有文件或路径 可以进入下一步
#在终端输入命令
ssh-keygen -t rsa -C "你的github邮箱地址"
#点击回车。生成一对密匙  存放在/users/yonghu/.ssh/
#私匙（id—rsa）公匙（id—rsa.pub）

3创建ssh key链接到github上面

settings→Account settings→SSH and GPG keys

新建New SSH key选项；在终端输入cd ~/.ssh/在终端显示key文件的list然后编辑id_rsa.pub将所有内容粘贴到github到key上面然后add ssh key

然后输出ssh -T git@github.com如果成功就可以在git congfig里面设置自己的登陆名字和邮箱具体命令为：

git config --global user.name "your name"

git config --global user.email "your_email@youremail.com"

4.克隆新建的项目到本地可以使用git clone https://项目地址
git clone ssh://git@192.168.3.209:10022/shuqian/shuqianjj.git #git克隆项目

5.上传操作

git init（初始化）

git add .（注意git add .中的“ .”把文件夹所有的文件加入要上传的文件夹中）

git commit -m 'first commit'（第一次提交修改）

git remote add origin https://github.com/YihangRan/ZZQ1908.git
（这是新建仓库的http地址，查看自己的仓库的地址如下图，点击Clone or download按钮，复制即可）

git push -u origin master（执行这一步的时候会让你输入git的账号和密码）

端口号为10022目前 用户为418483467@qq.com  密码为：123456

github上传出现问题时：报错
git错误：error: failed to push some refs to
解决办法：
发现是由于远程仓库中代码版本与本地不一致冲突导致的。
git pull
再自动merge或手动merge冲突
再次git push
成功解决问题

`https://docs.github.com/cn/get-started/getting-started-with-git/managing-remote-repositories #为官方学习文档`
