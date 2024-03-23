## 在Windows环境中安装git

网址：https://git-for-windows.github.io/ ，一路默认OK即可。



## 配置身份

首先第一件事打开Git Bash, 输入一下命令，提交的时候识别身份

```bash
git config --global user.name "Jingwei Zhang"
git config --global user.email "993987093@qq.com"
```


## 配置代理

如果您正在使用127.0.0.1的代理服务器和7890的端口

```bash
git config --global http.proxy 127.0.0.1:7890
```


## Github上的准备工作

在Github上新建一个仓库（Repository），注意不要带有README.md的



## 常用git命令

- git clone git地址

  指定branch

  git clone -b zjw https://github.com/seujingwei/DPU-PYNQ.git

- git push origin 分支名称

  -f可以强推但不推荐，最好使用其他分支保存，然后再推 

- git add 文件或目录

  把所有文件都加进去

  git add .

- git clean -f     清除未登记的文件

  git clean -fd  清除未登记的文件和目录

- git rm 文件或目录

  删除所有文件

  git rm -r .

  删除暂存区的文件

  git rm --cached 文件

- git checkout -- 文件

  回退文件

- git commit -m '备注说明'

  修改好的暂存区的文件打上备注，才可以push

- git reset HEAD或版本号

  版本号看 reflog的记录，并且reset之后，数据是存在暂存区的，需要重新commit

  git reset 1e0af1 --hard  强行复原，接git pull 可以不保留修改 回复状态

- git reflog  看提交的记录，带有版本号

- git log  根据commit查看操作

- git log --oneline  查看第一条，即版本的验证码

- git status

  看暂存区的修改文件 

- git branch 分支名称

  新建branch

  git branch zjw

  删除branch

  git branch -d zjw

  查看所有的branch包含远程仓库的

  git branch -a

- git branch --set-upstream-to=origin/分支名称 分支名称

- git checkout 分支名称

  跳转到对应分支

  git checkout zjw

- git checkout -b 分支名称 origin/分支名称

- git diff 版本1 版本2

- git merge 分支名称

  把分支合并

- git pull origin branch 从服务器的branch获取，合并到当前的本地branch

  相当于fetch + merge

  fetch是可以指定分支存到temp

  git fetch origin master:temp

- git tag 标签名称

- git stash  把本地文件保存为快照，这样git pull不会阻止

  git stash pop  查看快照 修改冲突

- git remote -v  查看当前远程库的地址

- git remote set-url origin ip地址  修改远程本地仓库的仓库地址

  git remote add mainline  https://github.com/Xilinx/DPU-PYNQ.git 增加一个远程仓库
  git remote set-url origin <new url>

- git rebase  复制commit

## 子模块相关操作

**0、切换子模块的链接**

```
cd [submodule folder]
git fetch origin
git pull
git checkout -b v1.2.1 tags/v1.2.1
cd ..
git add [submodule folder]
```

**1、创建子模块时指定一个分支**

通过 **-b** 指定对应分支

```
git submodule add -b master [URL to Git repo];
例如：git submodule add --force -b origin/v1.2.1 https://github.com/Xilinx/Vitis-AI.git vitis-ai-git/ --force表示强制添加
```

**2、子模块更新**

```sh
git submodule update --init --recursive
```

**3、删除子模块**

有时子模块的项目维护地址发生了变化，或者需要替换子模块，就需要删除原有的子模块。

删除子模块较复杂，步骤如下：

1. `rm -rf 子模块目录` 删除子模块目录及源码

2. `vi .gitmodules` 删除项目目录下.gitmodules文件中子模块相关条目

3. `vi .git/config` 删除配置项中子模块相关条目

4. `rm .git/module/*` 删除模块下的子模块目录，每个子模块对应一个目录，注意只删除对应的子模块目录即可

5. 执行完成后，再执行添加子模块命令即可，如果仍然报错，执行如下：

   ```
   git rm --cached 子模块名称
   ```

## 参考网址

同步项目到远程并解决冲突：

https://www.cnblogs.com/yehaia1/archive/2019/04/16/10715741.html

远程同步到本地：（是周期性同步而不是每次都clone，做法是通过fetch到temp，然后对操作分支进行merge）

https://blog.csdn.net/s740556472/article/details/80087026?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~first_rank_v2~rank_v28-1-80087026.nonecase&utm_term=github%E6%8B%89%E5%8F%96%E5%85%B6%E4%BB%96%E5%88%86%E6%94%AF%E6%9C%80%E6%96%B0%E4%BB%A3%E7%A0%81&spm=1000.2123.3001.4430

git pull 更新错误解决方法：

http://blog.chinaunix.net/uid-10415985-id-4142896.html

Git简单教程：

https://blog.csdn.net/qq_30848071/article/details/79460081
