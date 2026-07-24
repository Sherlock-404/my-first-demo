# Git + GitHub 入门阶段总结

---

# 一、Git 是什么？

## Git

Git 是一个**版本控制工具**。

作用：

* 记录代码变化
* 保存历史版本
* 查看修改内容
* 回退错误修改
* 多人协作开发

例如：

```text
代码 v1
  ↓
修改
  ↓
代码 v2
  ↓
修改
  ↓
代码 v3
```

Git 会记录每一个版本。

---

# 二、GitHub 是什么？

GitHub 是一个**代码托管平台**。

作用：

* 保存 Git 仓库
* 和别人共享代码
* 团队协作
* 开源项目管理

关系：

```text
Git
 |
 | 管理版本
 ↓
本地电脑

GitHub
 |
 | 保存远程仓库
 ↓
云端服务器
```

---

# 三、Git 安装和环境配置



## 1. 安装 Git

## 2. 配置环境变量

## 3. 配置 Git 用户信息

Git 提交需要知道作者是谁。

例如：

```bash
git config --global user.name "你的名字"

git config --global user.email "你的邮箱"
```

查看：

```bash
git config --list
```

---

# 四、SSH 密钥配置

## SSH 是什么？

SSH 是一种安全连接方式。

作用：

```text
电脑
 |
 | SSH认证
 ↓
GitHub
```

不用每次输入账号密码。

---

## 密钥组成

生成后得到：

```text
~/.ssh
│
├── id_ed25519        私钥
└── id_ed25519.pub    公钥
```

---

## 公钥和私钥区别

### 私钥

```text
id_ed25519
```
---

### 公钥

```text
id_ed25519.pub
```

* 可以上传 GitHub
* 用来验证身份

---

连接测试：

```bash
ssh -T git@github.com
```

成功说明：电脑已经信任 GitHub。

---

# 五、创建第一个 GitHub 项目

例如我的项目：

```text
my-first-demo
```

位置：

```text
D:\git\my-first-demo
```

---

## 本地创建仓库

进入目录：

```bash
cd /d/git/my-first-demo
```

初始化：

```bash
git init
```

用来创建目录：

```text
.git
```
表示：这个文件夹开始由 Git 管理。

---

# 六、Git 基础工作流程

```text
创建文件
    ↓
git status
    ↓
git add
    ↓
git commit
    ↓
git push
    ↓
GitHub
```

---

## 1. 查看状态

命令：

```bash
git status
```
---

## 2. 添加文件

命令：

```bash
git add .
```

作用是把文件放入暂存区（staging area）


---

## 3. 提交版本

命令：

```bash
git commit -m "说明"
```

作用：创建一个版本记录。

---

## 4. 上传 GitHub

第一次：

```bash
git push -u origin main
```

以后：

```bash
git push
```

---

# 七、远程仓库连接
连接本地仓库到远程仓库

添加 GitHub 地址：

```bash
git remote add origin 仓库地址
```

查看：

```bash
git remote -v
```

---

# 八、README.md

README 是项目说明文件。

---

# 九、同步问题-理解本地仓库与远程仓库

GitHub 修改了 README，但是 VS Code 没变化。

原因：Git 项目通常有两个部分：

本地仓库:位于自己电脑文件夹
负责：

* 写代码
* 修改文件
* 创建 commit

---

远程仓库：位于github
负责：

* 云端保存
* 团队共享
* 备份代码
---

Git 不会自动同步。

GitHub → 本地：

```bash
git pull
```

下载远程更新。

---

本地 → GitHub：

```bash
git push
```

上传本地修改。

---

# 十、查看历史版本


## 查看提交历史

```bash
git log --oneline
```
---

## 查看修改内容

命令：

```bash
git diff
```

作用：查看修改但还没有提交的内容

---

# 十一、git remote：管理远程仓库地址

远程仓库通常叫：

```text
origin
```

查看：

```bash
git remote -v
```

---

## 添加远程仓库

命令：

```bash
git remote add origin 仓库地址
```

---

## 删除远程仓库连接

命令：

```bash
git remote remove origin
```

作用：

```text
本地项目
       |
       X
       |
GitHub仓库
```

注意：

它只删除连接关系，不影响本地项目。

---

## 修改远程仓库地址

如果连接错了，可以：

删除：

```bash
git remote remove origin
```

重新添加：

```bash
git remote add origin 新地址
```

---

# 十二、什么时候用 clone？

如果GitHub 已经存在项目

```bash
git clone 仓库地址
```

流程：

```text
GitHub已有项目

        ↓

git clone

        ↓

本地开发

        ↓

git push
```

---

# Git 分支进阶总结

## 一、分支的作用

分支用于在不影响主代码的情况下，独立开发新功能。

---

# 二、分支常用命令

## 查看分支

```bash
git branch
```

例如：

```text
  dev
* main
```

含义：

* `dev`：存在的分支
* `*`：当前所在分支

---

## 创建分支

```bash
git branch dev
```
---

## 切换分支

```bash
git switch dev
```

---
## 创建并切换分支

推荐：

```bash
git switch -c dev
```
---
# 三、merge 合并分支

作用：

把一个分支的代码合并到当前分支。
* 一定要在main分支执行合并 
例如：

现在：

```text
main

A---B


dev

A---B---C
```

执行：

```bash
git switch main

git merge dev
```

结果：

```text
main

A---B---C
```

---

# 四、什么是冲突（Conflict）

两个分支修改了同一个位置，Git 不知道要保留哪一个所以停止合并

---

# 五、冲突文件里的特殊标记

## HEAD

表示：当前所在分支。

## =======

分隔线，上面：当前分支；下面：被合并分支。

---

## >>>>>>> dev

表示：dev 分支内容结束。

---

# 六、解决冲突流程

手动选择保留哪个，然后add并commit

```bash
git commit -m "解决冲突"
```
---

# Git 进阶学习笔记

## 一、git diff —— 查看文件修改

### 作用

查看文件具体修改了什么内容
---

### 使用流程
```bash
//revise
git status
//show modified: README.md
git diff
```
---

# 二、git restore —— 撤销未提交修改

## 作用

恢复已修改，但是还没有提交的文件，即恢复到最近一次 commit 的状态

---

## 注意

`git restore` 只能处理工作区；也就是：

```
修改文件
↓
git restore
↓
恢复
```

如果已经：

```bash
git add
```

需要：

```bash
git restore --staged 文件名
```

取消暂存。

---

# 三、git reset —— 撤销提交

## 作用

处理已经 commit，但是想撤销的修改

# reset 三种模式

## 1. --soft

命令：

```bash
git reset --soft HEAD~1
```

效果：

```
删除commit
保留修改
保留add状态
```
---

## 2. --mixed（默认）

命令：

```bash
git reset HEAD~1
```

效果：

```
删除commit
保留文件修改
取消add状态
```

状态：modified

---

## 3. --hard（慎用）

命令：

```bash
git reset --hard HEAD~1
```

效果：

```
删除commit
删除修改内容
```

---

# 四、HEAD 的含义

HEAD表示当前所在版本
HEAD~1表示上一个版本

---

# 五、git show —— 查看某次提交内容

命令：

```bash
git show commit_id
```
---

# 六、git fetch —— 获取远程信息

命令：

```bash
git fetch
```

作用：从 GitHub 获取最新信息。

# 七、查看远程缺少的提交

```bash
git log HEAD..origin/main --oneline
```
---

# 八、git rebase 

```bash
git pull --rebase
```

作用：把自己的提交移动到最新代码之后。

原来：

```
      C
     /
A---B
     \
      D
```

rebase：

```
A---B---C---D
```

优点：

提交历史更干净。

---
# 九、git revert

## 1. 为什么需要团队撤销？

在团队开发中，代码通常已经：

* 提交到远程仓库（GitHub）
* 被其他成员拉取使用

这时候不能随意修改历史，否则会影响其他人的代码同步。

因此推荐使用：

```bash
git revert
```

---

## 2. git revert 的作用

**创建一个新的提交，用来撤销之前某次提交的修改。**

例如：

原历史：

```text
A —— B —— C
```

C 提交有问题。

执行：

```bash
git revert C
```

结果：

```text
A —— B —— C —— D
```

其中：

* C：错误提交（保留）
* D：撤销 C 的新提交

---

## 3. 为什么团队更推荐 revert？

因为：

? 不删除历史
? 不改变提交记录
? 不影响其他开发者同步
? 方便查看项目变化过程

## 4. 常用流程

查看提交：

```bash
git log --oneline
```

选择需要撤销的提交：

```bash
git revert commit_id
```

完成后：

```bash
git push
```

---


