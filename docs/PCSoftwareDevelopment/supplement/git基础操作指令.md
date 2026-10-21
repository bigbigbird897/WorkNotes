# Git 基础操作

> 先区分：**工作区(写代码) → 暂存区(stage) → 本地仓库(local) → 远程仓库(remote)**

## 一、配置（首次使用git）

```
# 设置用户名、邮箱（提交记录会带上）
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"

# 查看配置
git config --list
```

`--global` 全局配置，对本机所有git项目生效；去掉则只针对当前项目。

## 二、创建/获取仓库

```
# 1.把本地文件夹变成git仓库（初始化）
git init

# 2.克隆远程仓库到本地
git clone shturl.cc/TEqmAloAB5I4MFVDQd6
```

## 三、日常核心流程

1. 修改文件（工作区）
2. 添加到暂存区

```
# 添加单个文件
git add filename.py

# 添加所有改动文件
git add .
```

1. 提交到**本地仓库**

```
git commit -m "提交说明：修复登录bug"
```

1. 推送到**远程仓库**

```
git push origin main
# origin：远程仓库别名；main：分支名，老项目可能是master
```

## 四、查看状态与日志

```
# 查看当前文件状态：哪些修改、哪些未暂存
git status

# 查看提交日志
git log

# 简洁版日志
git log --oneline
```

## 五、拉取远程代码

```
# 获取远程更新并合并到本地
git pull origin main

# 等价于 git fetch + git merge
# git fetch：只下载远程更新，不自动合并
git fetch origin
```

## 六、分支操作（高频）

```
# 查看本地分支
git branch

# 创建新分支
git branch dev

# 切换分支
git checkout dev
# 新版git也可以用
git switch dev

# 创建并立刻切换到新分支
git checkout -b dev
# 新版
git switch -c dev

# 合并分支：把dev合并到main，先切到main
git checkout main
git merge dev

# 删除本地分支
git branch -d dev

# 删除远程分支
git push origin --delete dev
```

## 七、撤销/回滚操作（非常常用）

```
# 1.工作区修改还没add：撤销文件修改，回到上次暂存/提交状态
git checkout -- filename.py

# 2.已经add到暂存区，还没commit：撤销暂存，回到工作区
git reset HEAD filename.py

# 3.已经commit，还没push：回退到上一个版本，保留代码改动
git reset --soft HEAD^

# 4.已经commit，还没push：回退，丢弃本地改动（谨慎！）
git reset --hard HEAD^

# HEAD^ 代表上一个版本；也可以写commit id前7位
git reset --hard a1b2c3d
```

> ⚠️ `--hard` 会丢弃本地修改，不要随便用！

## 八、远程仓库管理

```
# 查看远程仓库地址
git remote -v

# 添加远程仓库，别名origin
git remote add origin shturl.cc/TEqmAloAB5I4MFVDQd6

# 修改远程地址
git remote set-url origin 新地址
```

## 九、简单工作流示例

```
git init
git add .
git commit -m "初始化项目"
git remote add origin xxx.git
git push -u origin main

# 后续改代码
git add .
git commit -m "xxx"
git pull   # 先拉，防止冲突
git push
```

## 十、冲突提示

合并/拉取出现冲突时，文件里会出现标记：

```
<<<<<<< HEAD
本地代码
=======
远程代码
>>>>>>> xxx
```

手动编辑文件，删掉标记，保留需要的代码，再：

```
git add .
git commit -m "解决合并冲突"
```

------

### 速记口诀

`add` 放到暂存，`commit` 存本地，`push` 推远程，`pull` 拿远程； 分支：`switch`切，`merge`合并；回退慎用 `--hard`。

如果你需要，我可以给你一份**常用Git速查表（markdown）**，或者讲解`.gitignore`忽略文件配置。