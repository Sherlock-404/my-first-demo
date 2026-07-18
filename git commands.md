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

简单理解：

> Git 就像代码的“时间机器”。

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

让你的电脑：

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

作用为查看：

* 新文件
* 修改文件
* 是否需要提交
---

## 2. 添加文件

命令：

```bash
git add .
```

作用是把文件放入：

> 暂存区（staging area）

流程：

```text
文件
 ↓
git add
 ↓
暂存区
```

---

## 3. 提交版本

命令：

```bash
git commit -m "说明"
```

作用：

创建一个版本记录。

例如：

```bash
git commit -m "添加hello.py"
```

意思：

保存这一次修改。

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


添加 GitHub 地址：

```bash
git remote add origin 仓库地址
```

查看：

```bash
git remote -v
```

例如：

```text
origin git@github.com:Beno1-Debug/my-first-demo.git
```

含义：

本地仓库：

```text
my-first-demo
```

连接：

```text
GitHub仓库
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

作用：

查看：

> 修改但还没有提交的内容

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

例如：

```text
origin git@github.com:Beno1-Debug/my-first-demo.git (fetch)

origin git@github.com:Beno1-Debug/my-first-demo.git (push)
```

含义：

当前项目连接：

```text
本地项目
    |
    ↓
GitHub/my-first-demo
```

---

## 添加远程仓库

命令：

```bash
git remote add origin 仓库地址
```

例如：

```bash
git remote add origin git@github.com:Beno1-Debug/test.git
```

---

## 删除远程仓库连接

命令：

```bash
git remote remove origin
```

作用：

删除：

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

如果：

> GitHub 已经存在项目

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
很好 ? 你已经完成了 Git 学习里比较关键的一关：**分支冲突处理**。

到这里，你已经不是“只会上传代码”的 Git 用户了，而是已经掌握了实际开发中的核心流程。

我们先总结一下你刚刚新增的知识。

---

# Git 分支进阶总结

## 一、分支的作用

分支用于：

> 在不影响主代码的情况下，独立开发新功能。

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
## 一定要在main分支执行合并
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

