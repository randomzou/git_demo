# 版本控制工具Git使用笔记
---
### 本地创建库与远端同步
```
#　建立本地git repos
zys@zys-Lenovo:~/git_workplace/github$ mkdir git_demo
zys@zys-Lenovo:~/git_workplace/github$ cd git_demo
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git init 
Initialized empty Git repository in /home/zys/git_workplace/github/git_demo/.git/
zys@zys-Lenovo:~/git_workplace/github/git_demo$ ll
total 12
drwxrwxr-x 3 zys zys 4096 Sep 20 17:16 ./
drwxrwxr-x 5 zys zys 4096 Sep 20 17:15 ../
drwxrwxr-x 7 zys zys 4096 Sep 20 17:16 .git/
zys@zys-Lenovo:~/git_workplace/github/git_demo$ ls ./git
ls: cannot access ./git: No such file or directory
zys@zys-Lenovo:~/git_workplace/github/git_demo$ ls .git/
branches  config  description  HEAD  hooks  info  objects  refs
```
### 本地关联远端repository新增文件并提交
- 将当前文件添加到index区
    - git add file, git add * # 所有文件
- 查看当前分支文件修改情况
    - git status : 
-　提交index区域文件到HEAD区域
    -　git commit -m " message "
        ![不同阶段工作代码状态][1]
```
zys@zys-Lenovo:~/git_workplace/github/git_demo$ touch README.md
zys@zys-Lenovo:~/git_workplace/github/git_demo$ vim README.md 
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git add README.md 
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.md
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git commit  -m "add README.md file"
[master (root-commit) 99345e3] add README.md file
 1 file changed, 1 insertion(+)
 create mode 100644 README.md

```

### 关联远端repository并上载到远端
- 在远端建立库来同步本地库
<center>![{C6FF807B-0F52-4D51-B286-515A847DB6A9}.png-57.6kB][3]</center＞
- 本地库与远程库关联
    - git remote add origin https://github.com/randomzou/git_demo.git
    - https or ssh 模式
- 更新文件
    - git push -u origin master
    - origin:远端默认repository名, master: 默认主分支名git repository,上传文件
```
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git remote add origin https://github.com/randomzou/git_demo.git
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git push -u origin master
Username for 'https://github.com': randomzou
Password for 'https://randomzou@github.com': 
Counting objects: 3, done.
Writing objects: 100% (3/3), 251 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/randomzou/git_demo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```
### 创建分支

- git branch branch_name
```
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git branch git_demo_b1
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git checkout git_demo_b1 
Switched to branch 'git_demo_b1'
zys@zys-Lenovo:~/git_workplace/github/git_demo$ ls
README.md
```
### 更新本地库至最新
- 在远端建立文件，本地拉取远端当前最新版本更新本地版本
    - git pull
        - git fetch
        - git merge
```
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git checkout master 
Switched to branch 'master'
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git pull
Updating 99345e3..a207175
Fast-forward
 remote_new.txt | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 remote_new.txt
```
### merge 数据
```
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git checkout git_demo_b1 
Switched to branch 'git_demo_b1'
zys@zys-Lenovo:~/git_workplace/github/git_demo$ ls
README.md
zys@zys-Lenovo:~/git_workplace/github/git_demo$ mkdir branch_dir
zys@zys-Lenovo:~/git_workplace/github/git_demo$ cd branch_dir/
zys@zys-Lenovo:~/git_workplace/github/git_demo/branch_dir$ touch branch_own.txt
zys@zys-Lenovo:~/git_workplace/github/git_demo/branch_dir$ vim branch_own.txt 
zys@zys-Lenovo:~/git_workplace/github/git_demo/branch_dir$ cd ..
zys@zys-Lenovo:~/git_workplace/github/git_demo$ ls
branch_dir  README.md
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git merge master 
Updating 99345e3..a207175
Fast-forward
 remote_new.txt | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 remote_new.txt
zys@zys-Lenovo:~/git_workplace/github/git_demo$ ls
branch_dir  README.md  remote_new.txt
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git commit  -m "git_demo_b1 add file"
[git_demo_b1 f4af7b6] git_demo_b1 add file
 1 file changed, 1 insertion(+)
 create mode 100644 branch_dir/branch_own.txt
```

### 比较文件区别
 - git diff source_branch  target_branch
```
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git diff git_demo_b1  master 
diff --git a/branch_dir/branch_own.txt b/branch_dir/branch_own.txt
deleted file mode 100644
index 7f8f656..0000000
--- a/branch_dir/branch_own.txt
+++ /dev/null
@@ -1 +0,0 @@
-# 当前分支独有文件
zys@zys-Lenovo:~/git_workplace/github/git_demo$ git push origin git_demo_b1 
Username for 'https://github.com': randomzou 
Password for 'https://randomzou@github.com': 
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 403 bytes | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To https://github.com/randomzou/git_demo.git
 * [new branch]      git_demo_b1 -> git_demo_b1
```
![{05A3413F-550F-4614-8407-A3B476201215}.png-53kB][4]

- http://rogerdudler.github.io/git-guide/index.zh.html

  [1]: http://rogerdudler.github.io/git-guide/img/trees.png
  [2]: http://rogerdudler.github.io/git-guide/img/treesstatic.zybuluo.com/randomxy/e0xcg9hbfas20m95ootd6yac/%7B05A3413F-550F-4614-8407-A3B476201215%7D.png
  [3]: http://static.zybuluo.com/randomxy/z53kt5ci348odw4ub0f4bvwh/%7BC6FF807B-0F52-4D51-B286-515A847DB6A9%7D.png
  [4]: http://static.zybuluo.com/randomxy/jpmg1628ntipzgbtbuep7boq/%7B05A3413F-550F-4614-8407-A3B476201215%7D.png
