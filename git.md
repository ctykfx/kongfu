1. git

```
1. 命令行工具：git for windows
https://git-for-windows.github.io/

2. 可视化工具：TortoiseGit
https://tortoisegit.org

3. idea插件

4. github网站
http://www.github.com
```

2. 配置git签名

   2.1 第一步

   ```
   1. 选中你要作为git工程存放的目录，然后单击鼠标右键选择git bash即可
   
   tip:
   git是分布式版本控制工具，所以需要我们填写用户名和邮箱作为一个标志。
   C:\Users\xxx\路径下.gitconfig文件，这个文件里面可以看到--global属性，所有的git项目都会公用这个属性
   
   git config --global user.name "kfx"
   git config --global user.email "xxx.com"
   ```

3. 创建版本库

   3.1 第一步 选中一个git工程的目录

   3.2 第二步 输入命令初始化版本库

   ```
   git init
   ```

4. git命令行操作

   4.1 查看文件状态

   ```
   git status
   ```

   4.2 将文件/目录添加到临时暂存区
   
   ```
   git add 文件名/目录名
   e.g.
   git add src/
   
   tip：
   以上通过git add命令的文件会提交到暂存区，但是这里的文件其实是没有真正的提交，使用下一个命令才是把它提交到一个统一的版本文件
   ```
   
   4.3 提交文件
   
   ```
   git commit 
   
   e.g.
   git commit -m '提交提示信息'
   
   tip:
   每当有文件被修改/添加/删除时，都需要重新git add，然后再git commit
   ```
   
   4.4 查看日志
   
   ```
   git log :查看历史记录
   
   e.g.
   $ git log
   commit c64e250b2d4d452aeaf981e2ce27650ccf2cf5c7 (HEAD -> master)
   Author: kfx <xxx.com>
   Date:   Tue Apr 27 23:20:53 2021 +0800
   
       update 1.txt
   
   commit 4e4ff4aad689b05cfd03ae9a5f60409830d4cc28
   Author: kfx <xxx.com>
   Date:   Tue Apr 27 23:14:43 2021 +0800
   
       creat 001
   
   e.g.
   $ git log --pretty=oneline
   c64e250b2d4d452aeaf981e2ce27650ccf2cf5c7 (HEAD -> master) update 1.txt
   4e4ff4aad689b05cfd03ae9a5f60409830d4cc28 creat 001
   
   ```
   
   4.5 回退历史
   
   4.5.1 创建一个文件：a.txt
   
   ```
   aa
   bb
   cc
   dd
   
   tip:
   添加到暂存区然后提交
   ```
   
   4.5.2 修改这个文件：a.txt
   
   ```
   aa
   cc
   dd
   ee
   
   tip:
   添加到暂存区然后提交
   ```
   
   4.5.3 回退到上一次提交
   
   ```
   git reset --hard HEAD^1
   
   tip:
   HEAD是一个指针，永远指向最新版本，^1表示让HEAD指针指向上一个版本
   
   --hard 硬：这种回退不但版本回退，还指定的数据抹除，不会保留任何已修改的记录
   --soft 软：回退版本，也会保留改动的记录。会自动帮你git add
   --mix 折中：回退版本，并会保留所有改动记录，但是不会自动帮你git add
   
   git reset ：修改HEAD的位置
   
   这种方式可以恢复到之前某个提交的版本，但是恢复之后，当前版本之后的版本将不复存在。
   ```
   
   4.5.4 回退到多个版本
   
   ```
   git reset --hard HEAD~2  # 回退两个版本
   ```
   
   4.5.5 版本穿越
   
   ```
   git reflog # 查看历史记录的版本号
   
   e.g.
   c0b2026 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~2
   c4cffb7 HEAD@{1}: commit: update 002
   357a862 HEAD@{2}: commit: update 001
   c0b2026 (HEAD -> master) HEAD@{3}: commit: creat 002
   4e4ff4a HEAD@{4}: reset: moving to HEAD^1
   c64e250 HEAD@{5}: reset: moving to HEAD^1
   f40436e HEAD@{6}: reset: moving to HEAD^1
   211c313 HEAD@{7}: commit: creat 004
   f40436e HEAD@{8}: commit: creat 003
   c64e250 HEAD@{9}: commit: update 1.txt
   4e4ff4a HEAD@{10}: commit (initial): creat 001
   
   e.g.
   git reset --hard 211c313
   
   tip:
   英文状态下q退出
   ```
   
   4.6 还原文件
   
   ```
   git checkout 文件名
   
   e.g.
   vi src/b.txt
   111
   222
   333
   444
   555
   
   git add src/b.txt
   git commit -m 'update 008'
   
   修改b.txt
   111
   222
   333
   444
   
   git checkout src/b.txt
   111
   222
   333
   444
   555
   ```
   
   4.7 删除文件
   
   ```
   1. 删除文件
   2. git add
   3. git commit 
   ```
   
5. 工作区、暂存区、本地库

   5.1 概念

   ```
   工作区(working Directory):电脑的本地磁盘目录
   暂存区(Repostory):工作区中有一个隐藏目录.git,它是git的本地版本库
   本地库(Satge):一般存储在git目录下的index文件，所以我们把暂存区有时候也叫作索引
   ```

   5.2 关系图

   ![001](F:\code\001.png)

6. 分支

   6.1 

   ![002](F:\code\002.png)

   6.2 查看分支
   
   ```
   git branch -v
   
   e.g.
   $ git branch -v
   * master 06b2f8a update 0429 2202
   ```
   
   6.3 创建分支
   
   ```
   git branch 分支名称
   
   e.g.
   $ git branch feature_kfx
   $ git branch -v
     feature_kfx 06b2f8a update 0429 2202
   * master      06b2f8a update 0429 2202
   ```
   
   6.4 切换分支
   
   ```
   git checkout 分支名
   
   e.g.
   git checkout feature_kfx
   ```
   
   6.5 合并分支(将其他分支合并到主分支:master)
   
   ```
   1. 切换到主分支
   git checkout master
   
   2. 合并
   git merge 分支名
   
   e.g.
   git merge feature_kfx
   ```
   
7. 冲突

   7.1 什么是冲突

   ```
   冲突一般是指同一个文件同一个位置的代码，再两种版本的仓库合并时，版本的管理软件无法判断到底应该保留哪一个版本，因此会提示该文件发生冲突，冲突一般都需要手动解决。
   ```

   7.2 在分支合并的时候解决冲突

   ```
   1. 先在master上建一个kfx.txt
   2. 再在festure_kfx上建一个kfx.txt
   3. 分别提交
   4. 最后合并
   
   e.g.
   $ git merge feature_kfx
   CONFLICT (add/add): Merge conflict in kfx.txt
   Auto-merging kfx.txt
   Automatic merge failed; fix conflicts and then commit the result.
   
   5. 查看冲突
   git diff
   
   $ git diff
   diff --cc kfx.txt
   index c3c0de8,022801a..0000000
   --- a/kfx.txt
   +++ b/kfx.txt
   @@@ -1,1 -1,1 +1,5 @@@
    -kxl
   ++<<<<<<< HEAD
    +kfx
   ++=======
   ++kxl
   ++>>>>>>> feature_kfx
   6. 解决冲突，切换到那个目录，然后查看文件
   7. 再重新add和commit即可解决冲突
   ```

8. GitHub

   8.1 什么是GitHub？

   ```
   github是一个git项目托管网站，主要提供基于git的版本托管服务。
   网址：https://github.com/
   
   - ctykfx 或者 k2311754999@163.com
   - Wokong222###
   
   注册账号注意事项
   - 较长时间不使用，有可能被github冻结账号
   - 如果冻结账号，请登录https://github.com/contact恢复申请
   ```

   tips:
   github登录不上

   > 1. IP查询网站：https://www.ipaddress.com/
   >
   >    ![003](F:\code\003.png)
   >
   > 2. 依次点击github.com  https://github.com.ipaddress.com/  获取ip1
   >
   >    ![004](F:\code\004.png)
   >
   > 3. 再次点击github.com  https://fastly.net.ipaddress.com/github.global.ssl.fastly.net  获取iP2
   >
   >    ![005](F:\code\005.png)
   >
   > 4. 写入hosts文件
   >
   >    > 复制 `C:\Windows\System32\drivers\etc` 路径下的 `hosts`文件至桌面，并修改hosts文件，加入如下内容：
   >
   >    ```
   >    140.82.114.4 github.com
   >    199.232.69.194 github.global.ssl.fastly.net
   >    ```
   >
   > 5. 刷新DNS
   >
   >    > 打开cmd,输入如下指令
   >
   >    ```text
   >    ipconfig /flushdns
   >    ```
   >
   > 6. 重启浏览器即可访问

   ![006](F:\code\006.png)

   

   8.2 Github操作

   8.2.1 建立本地仓库

   ```
   1. 创建guojing和huangrong子目录
   2. huangrong搭建代码库
   git init
   git config user.name "huangrong"
   git config user.email "2311754999@qq.com"
   
   3.提交代码
   git add
   git commit
   ```

   8.2.2 注册github账号并登录

   8.2.3 创建github的项目库

   ![007](F:\code\007.png)

   8.2.4 推送代码到github

   - 增加远程地址

   ```
   git remote add <远端代号> <远端地址>
   <远端代号> : 指远程链接的代号，一般直接使用origin作为代号，亦可以自定义
   <远端地址> : 指远程链接的url
   
   e.g.
   git remote add origin https://github.com/ctykfx/kongfu.git
   ```

   - 推送到远程库

   ```
   git push <远端代号> <分支名称>
   
   e.g.
   git push origin master
   ```

   