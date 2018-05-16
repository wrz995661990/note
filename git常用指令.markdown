# git常用指令
  
  ## 本地指令
    ```
    git init   初始化  在本地的当前目录里面初始化git仓库
    git status 查看当前状态，碰到问道不知道怎么办的时候，可以通过看它给出的提示来解决问题
    git clone （仓库的http地址或者ssh） 从网络上某个地址拷贝到本地
    git diff 查看当前状态和最新的commit之间有什么不同。
    git add -A 通用的在commit之前要add
    git checkout -- . 这里用小数点表示撤回所有修改，在 -- 的前后都有空格、
    git commit  -m “提交信息” 提交信息最好能体现更改了什么
    git clean -xf 删除当前目录下所有没有track过的文件。不管他是不是.gitigonre文件里指定的文件夹和文件
    git log 查看当前版本以及之前的commit记录
    git reflog  head的变更记录
    git reset --hard 版本号   回退到指定版本号的版本，该版本之后的修改都被删除。同时也是通过这个命令回到最新版本。需要reflog配合 
    
    ```
  ## 远程仓库指令
    ```
    git config --global user.name "用户名"
    git config --global user.email "邮箱"
    ssh-keygen -t rsa -C "邮箱"  这条命令前面不用加git
    git remote add origin "地址" 设置origin
    git push -u origin master 指定origin为默认主机，以后push默认上传到origin上
    git push 将当前分支增加的commit提交到远程仓库
    git pull 在本地版本低于远程仓库版本的时候，获取远程仓库的commit
    
    ```
    
    [参考学习资料](http://www.cnblogs.com/schaepher/p/5561193.html)
    
    
