# Git 实用指南

本指南面向日常 GitHub 项目操作，重点罗列常用命令、典型工作流、撤销方法和常见报错处理。默认已安装 Git，并在终端中进入项目目录。

---

## 1. 初始配置

### 查看 Git 版本

```bash
git --version
```

### 设置用户名和邮箱

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

查看配置：

```bash
git config --global --list
```

查看单项配置：

```bash
git config --global user.name
git config --global user.email
```

仅为当前仓库设置用户名和邮箱：

```bash
git config user.name "Your Name"
git config user.email "your_email@example.com"
```

### 设置默认分支名

```bash
git config --global init.defaultBranch main
```

### 设置默认编辑器为 Nano

```bash
git config --global core.editor "nano"
```

设置为 VS Code：

```bash
git config --global core.editor "code --wait"
```

---

## 2. 创建或获取仓库

### 初始化当前目录

```bash
git init
```

### 初始化指定目录

```bash
git init project_name
```

### 克隆 GitHub 仓库

HTTPS：

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
```

SSH：

```bash
git clone git@github.com:USERNAME/REPOSITORY.git
```

指定本地目录名：

```bash
git clone https://github.com/USERNAME/REPOSITORY.git local_folder
```

克隆指定分支：

```bash
git clone -b branch_name https://github.com/USERNAME/REPOSITORY.git
```

浅克隆，只下载最近一次提交：

```bash
git clone --depth 1 https://github.com/USERNAME/REPOSITORY.git
```

克隆包含子模块的仓库：

```bash
git clone --recurse-submodules https://github.com/USERNAME/REPOSITORY.git
```

已有仓库补拉子模块：

```bash
git submodule update --init --recursive
```

---

## 3. 查看仓库状态

### 查看当前状态

```bash
git status
```

简洁显示：

```bash
git status -s
```

常见状态标记：

```text
??  未跟踪文件
M   已修改文件
A   已暂存的新文件
D   已删除文件
R   已重命名文件
```

### 查看当前分支

```bash
git branch --show-current
```

### 查看所有本地分支

```bash
git branch
```

### 查看本地和远程分支

```bash
git branch -a
```

---

## 4. 查看修改内容

### 查看未暂存修改

```bash
git diff
```

查看指定文件：

```bash
git diff path/to/file.py
```

### 查看已暂存修改

```bash
git diff --staged
```

等价命令：

```bash
git diff --cached
```

### 查看与最近一次提交的全部差异

```bash
git diff HEAD
```

### 查看两个提交之间的差异

```bash
git diff COMMIT_A COMMIT_B
```

### 查看两个分支之间的差异

```bash
git diff branch_a branch_b
```

### 只查看发生变化的文件名

```bash
git diff --name-only
```

### 查看修改统计

```bash
git diff --stat
```

---

## 5. 添加文件到暂存区：`git add`

### 添加单个文件

```bash
git add file.py
```

### 添加多个文件

```bash
git add file1.py file2.py README.md
```

### 添加某个目录

```bash
git add src/
```

### 添加当前目录下所有变化

```bash
git add .
```

### 添加整个仓库中的所有变化

```bash
git add -A
```

### 只添加已被 Git 跟踪文件的修改和删除

```bash
git add -u
```

### 交互式选择修改片段

```bash
git add -p
```

常用交互选项：

```text
y  暂存当前片段
n  不暂存当前片段
s  将当前片段继续拆分
q  退出
a  暂存当前文件后续所有片段
d  不暂存当前文件后续所有片段
```

### 将删除操作加入暂存区

```bash
git add -u
```

或者：

```bash
git rm file.txt
```

---

## 6. 取消暂存

### 取消暂存单个文件

```bash
git restore --staged file.py
```

### 取消暂存全部文件

```bash
git restore --staged .
```

旧版写法：

```bash
git reset HEAD file.py
```

取消暂存不会删除工作区中的修改。

---

## 7. 提交修改：`git commit`

### 提交暂存区内容

```bash
git commit -m "描述本次修改"
```

示例：

```bash
git commit -m "Add PiperX joint limit validation"
```

### 打开编辑器填写提交信息

```bash
git commit
```

### 自动暂存已跟踪文件并提交

```bash
git commit -am "Fix control mode switching"
```

注意：

```bash
git commit -am
```

不会包含未被 Git 跟踪的新文件。新文件仍需先执行：

```bash
git add new_file.py
```

### 修改最近一次提交信息

```bash
git commit --amend -m "新的提交信息"
```

### 将新修改补进最近一次提交

```bash
git add .
git commit --amend --no-edit
```

如果最近一次提交已经推送到远程，修改后通常需要：

```bash
git push --force-with-lease
```

不要在多人共享分支上随意改写已经推送的提交历史。

### 创建空提交

```bash
git commit --allow-empty -m "Trigger CI"
```

---

## 8. 查看提交历史

### 查看完整日志

```bash
git log
```

### 单行显示

```bash
git log --oneline
```

### 图形化显示分支历史

```bash
git log --oneline --graph --decorate --all
```

### 查看最近 5 次提交

```bash
git log -5
```

### 查看某个文件的提交历史

```bash
git log -- path/to/file.py
```

### 查看每次提交的修改内容

```bash
git log -p
```

### 查看每次提交的统计

```bash
git log --stat
```

### 按作者筛选

```bash
git log --author="Name"
```

### 按提交信息筛选

```bash
git log --grep="keyword"
```

### 查看某次提交详情

```bash
git show COMMIT_HASH
```

查看某次提交中的指定文件：

```bash
git show COMMIT_HASH:path/to/file.py
```

---

## 9. 连接远程 GitHub 仓库

### 查看远程仓库

```bash
git remote -v
```

### 添加远程仓库

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
```

SSH：

```bash
git remote add origin git@github.com:USERNAME/REPOSITORY.git
```

### 修改远程仓库地址

```bash
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

改为 SSH：

```bash
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

### 查看远程仓库详细信息

```bash
git remote show origin
```

### 删除远程仓库

```bash
git remote remove origin
```

### 重命名远程仓库

```bash
git remote rename origin upstream
```

---

## 10. 推送到 GitHub：`git push`

### 第一次推送当前分支

```bash
git push -u origin main
```

`-u` 会建立当前本地分支与远程分支的跟踪关系。之后可直接使用：

```bash
git push
```

### 推送指定分支

```bash
git push origin branch_name
```

### 推送所有本地分支

```bash
git push --all origin
```

### 推送标签

```bash
git push origin tag_name
```

推送全部标签：

```bash
git push origin --tags
```

### 删除远程分支

```bash
git push origin --delete branch_name
```

### 安全强制推送

```bash
git push --force-with-lease
```

不推荐直接使用：

```bash
git push --force
```

### 推送当前分支并自动设置上游

```bash
git push -u origin HEAD
```

---

## 11. 从 GitHub 获取更新

### 获取远程更新但不合并

```bash
git fetch
```

获取指定远程仓库：

```bash
git fetch origin
```

获取并清理已删除的远程分支引用：

```bash
git fetch --prune
```

### 拉取并合并

```bash
git pull
```

指定远程分支：

```bash
git pull origin main
```

### 使用 Rebase 方式拉取

```bash
git pull --rebase
```

指定分支：

```bash
git pull --rebase origin main
```

### 只允许快进合并

```bash
git pull --ff-only
```

### 推荐的安全同步方式

```bash
git status
git fetch origin
git pull --rebase origin main
```

如果本地有未提交修改，可先：

```bash
git stash
git pull --rebase
git stash pop
```

---

## 12. 分支操作

### 创建分支

```bash
git branch branch_name
```

### 切换分支

```bash
git switch branch_name
```

旧版写法：

```bash
git checkout branch_name
```

### 创建并切换分支

```bash
git switch -c branch_name
```

旧版写法：

```bash
git checkout -b branch_name
```

### 基于指定分支创建新分支

```bash
git switch -c feature_branch main
```

### 基于远程分支创建本地分支

```bash
git switch -c branch_name --track origin/branch_name
```

也可以：

```bash
git switch branch_name
```

较新的 Git 通常会自动创建对应的本地跟踪分支。

### 重命名当前分支

```bash
git branch -m new_name
```

### 重命名指定分支

```bash
git branch -m old_name new_name
```

### 删除已合并的本地分支

```bash
git branch -d branch_name
```

### 强制删除本地分支

```bash
git branch -D branch_name
```

### 查看分支跟踪关系

```bash
git branch -vv
```

### 设置上游分支

```bash
git branch --set-upstream-to=origin/main main
```

或者首次推送时：

```bash
git push -u origin main
```

---

## 13. 合并分支

### 将目标分支合并到当前分支

先切换到接收修改的分支：

```bash
git switch main
```

再合并：

```bash
git merge feature_branch
```

### 创建明确的合并提交

```bash
git merge --no-ff feature_branch
```

### 中止合并

```bash
git merge --abort
```

### 删除合并后的分支

```bash
git branch -d feature_branch
git push origin --delete feature_branch
```

---

## 14. Rebase 操作

### 将当前分支变基到主分支

```bash
git switch feature_branch
git rebase main
```

### 将当前分支变基到远程主分支

```bash
git fetch origin
git rebase origin/main
```

### 处理冲突后继续

```bash
git add conflicted_file.py
git rebase --continue
```

### 跳过当前提交

```bash
git rebase --skip
```

### 中止 Rebase

```bash
git rebase --abort
```

### 交互式整理最近 3 次提交

```bash
git rebase -i HEAD~3
```

常用操作：

```text
pick    保留提交
reword  修改提交信息
edit    修改提交内容
squash  合并到前一个提交并编辑提交信息
fixup   合并到前一个提交并丢弃当前提交信息
drop    删除提交
```

已经推送到共享分支的提交，不应随意使用 Rebase 改写历史。

---

## 15. 临时保存修改：`git stash`

### 暂存当前未提交修改

```bash
git stash
```

添加说明：

```bash
git stash push -m "Temporary PiperX changes"
```

### 同时暂存未跟踪文件

```bash
git stash -u
```

### 同时暂存被忽略文件

```bash
git stash -a
```

### 查看 Stash 列表

```bash
git stash list
```

### 恢复最近一次 Stash，但保留记录

```bash
git stash apply
```

### 恢复并删除最近一次 Stash

```bash
git stash pop
```

### 恢复指定 Stash

```bash
git stash apply stash@{1}
```

### 查看 Stash 内容

```bash
git stash show
```

查看详细差异：

```bash
git stash show -p stash@{0}
```

### 删除指定 Stash

```bash
git stash drop stash@{0}
```

### 清空所有 Stash

```bash
git stash clear
```

### 从 Stash 创建新分支

```bash
git stash branch new_branch stash@{0}
```

---

## 16. 撤销工作区修改：`git restore`

### 放弃单个文件的未暂存修改

```bash
git restore file.py
```

### 放弃全部未暂存修改

```bash
git restore .
```

### 恢复到指定提交中的版本

```bash
git restore --source COMMIT_HASH file.py
```

### 同时恢复工作区和暂存区

```bash
git restore --source HEAD --staged --worktree file.py
```

注意：`git restore` 会覆盖未提交修改，执行前应先确认。

---

## 17. 撤销提交：`reset`、`revert`

### 取消最近一次提交，保留修改在暂存区

```bash
git reset --soft HEAD~1
```

### 取消最近一次提交，保留修改但取消暂存

```bash
git reset HEAD~1
```

等价：

```bash
git reset --mixed HEAD~1
```

### 取消最近一次提交并删除修改

```bash
git reset --hard HEAD~1
```

### 回退到指定提交

```bash
git reset --hard COMMIT_HASH
```

### 撤销某次提交并生成新的反向提交

```bash
git revert COMMIT_HASH
```

撤销最近一次提交：

```bash
git revert HEAD
```

撤销多个提交：

```bash
git revert OLDEST_COMMIT^..NEWEST_COMMIT
```

使用建议：

- 未推送的个人提交：可使用 `git reset`
- 已推送的共享提交：优先使用 `git revert`
- `git reset --hard` 会永久丢弃未提交内容，应谨慎使用

---

## 18. 恢复误删的提交

### 查看操作历史

```bash
git reflog
```

示例：

```text
abc1234 HEAD@{0}: reset: moving to HEAD~1
def5678 HEAD@{1}: commit: Add robot client
```

恢复到之前提交：

```bash
git reset --hard def5678
```

或者新建恢复分支：

```bash
git switch -c recovery_branch def5678
```

---

## 19. 删除和重命名文件

### 删除文件并加入暂存区

```bash
git rm file.txt
```

### 删除目录

```bash
git rm -r folder/
```

### 仅从 Git 中删除，保留本地文件

```bash
git rm --cached file.txt
```

删除目录的跟踪但保留本地：

```bash
git rm -r --cached folder/
```

### 重命名文件

```bash
git mv old_name.py new_name.py
```

### 移动文件

```bash
git mv file.py src/file.py
```

然后提交：

```bash
git commit -m "Rename file"
```

---

## 20. `.gitignore`

### 创建 `.gitignore`

```bash
nano .gitignore
```

常见内容：

```gitignore
# Python
__pycache__/
*.py[cod]
*.egg-info/
.venv/
venv/

# Environment variables
.env
.env.*

# IDE
.vscode/
.idea/

# OS
.DS_Store

# Logs
*.log
logs/

# Model checkpoints
checkpoints/
*.ckpt
*.pth
*.pt

# Datasets
data/
datasets/

# Build output
build/
dist/

# Temporary files
*.tmp
*.swp
```

### 文件已被 Git 跟踪后再加入 `.gitignore`

仅写入 `.gitignore` 不会停止跟踪。需要执行：

```bash
git rm --cached file_name
```

目录：

```bash
git rm -r --cached folder_name
```

然后提交：

```bash
git add .gitignore
git commit -m "Update gitignore"
```

### 重新应用整个 `.gitignore`

```bash
git rm -r --cached .
git add .
git commit -m "Reapply gitignore"
```

### 检查文件为何被忽略

```bash
git check-ignore -v path/to/file
```

---

## 21. 标签操作

### 查看标签

```bash
git tag
```

### 创建轻量标签

```bash
git tag v1.0.0
```

### 创建带说明的标签

```bash
git tag -a v1.0.0 -m "Release v1.0.0"
```

### 为指定提交创建标签

```bash
git tag -a v1.0.0 COMMIT_HASH -m "Release v1.0.0"
```

### 查看标签信息

```bash
git show v1.0.0
```

### 推送标签

```bash
git push origin v1.0.0
```

推送全部标签：

```bash
git push origin --tags
```

### 删除本地标签

```bash
git tag -d v1.0.0
```

### 删除远程标签

```bash
git push origin --delete v1.0.0
```

---

## 22. Cherry-pick

### 将某个提交应用到当前分支

```bash
git cherry-pick COMMIT_HASH
```

### 应用多个提交

```bash
git cherry-pick COMMIT_A COMMIT_B
```

### 应用连续提交范围

```bash
git cherry-pick OLDEST_COMMIT^..NEWEST_COMMIT
```

### 处理冲突后继续

```bash
git add conflicted_file.py
git cherry-pick --continue
```

### 中止 Cherry-pick

```bash
git cherry-pick --abort
```

---

## 23. 处理合并冲突

发生冲突后：

```bash
git status
```

冲突文件中通常会出现：

```text
<<<<<<< HEAD
当前分支内容
=======
目标分支内容
>>>>>>> branch_name
```

处理步骤：

1. 打开冲突文件。
2. 删除冲突标记。
3. 保留正确内容。
4. 保存文件。
5. 将文件加入暂存区。
6. 继续当前操作。

合并冲突：

```bash
git add conflicted_file.py
git commit
```

Rebase 冲突：

```bash
git add conflicted_file.py
git rebase --continue
```

Cherry-pick 冲突：

```bash
git add conflicted_file.py
git cherry-pick --continue
```

查看仍有冲突的文件：

```bash
git diff --name-only --diff-filter=U
```

放弃合并：

```bash
git merge --abort
```

放弃 Rebase：

```bash
git rebase --abort
```

---

## 24. Fork 仓库同步上游

假设自己的 Fork 为 `origin`，原始仓库为 `upstream`。

### 添加上游仓库

```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/REPOSITORY.git
```

查看：

```bash
git remote -v
```

### 获取上游更新

```bash
git fetch upstream
```

### 将本地 main 同步到上游 main

```bash
git switch main
git fetch upstream
git rebase upstream/main
```

或者使用 merge：

```bash
git switch main
git fetch upstream
git merge upstream/main
```

### 推送到自己的 Fork

```bash
git push origin main
```

---

## 25. GitHub Pull Request 常用工作流

### 创建功能分支

```bash
git switch main
git pull --rebase origin main
git switch -c feature/piper-client
```

### 修改并提交

```bash
git status
git add .
git commit -m "Add PiperX policy client"
```

### 推送分支

```bash
git push -u origin feature/piper-client
```

然后在 GitHub 网页中创建 Pull Request。

### PR 更新后继续推送

```bash
git add .
git commit -m "Fix review comments"
git push
```

### PR 合并后清理本地分支

```bash
git switch main
git pull --rebase origin main
git branch -d feature/piper-client
git fetch --prune
```

删除远程分支：

```bash
git push origin --delete feature/piper-client
```

---

## 26. GitHub CLI 常用命令

安装并登录 GitHub CLI 后，可使用 `gh` 命令。

### 登录

```bash
gh auth login
```

查看登录状态：

```bash
gh auth status
```

### 克隆仓库

```bash
gh repo clone OWNER/REPOSITORY
```

### 创建 GitHub 仓库

```bash
gh repo create
```

在当前目录创建远程仓库并推送：

```bash
gh repo create repository_name --public --source=. --remote=origin --push
```

私有仓库：

```bash
gh repo create repository_name --private --source=. --remote=origin --push
```

### 创建 Pull Request

```bash
gh pr create
```

带标题和说明：

```bash
gh pr create --title "Add PiperX support" --body "Implements PiperX client."
```

### 查看 Pull Request

```bash
gh pr list
```

```bash
gh pr view
```

### 检出 Pull Request

```bash
gh pr checkout PR_NUMBER
```

### 合并 Pull Request

```bash
gh pr merge PR_NUMBER
```

### 查看 Issue

```bash
gh issue list
```

创建 Issue：

```bash
gh issue create
```

---

## 27. 常见完整工作流

### 场景一：修改已有仓库并推送

```bash
cd project
git status
git pull --rebase
git add .
git commit -m "Describe changes"
git push
```

### 场景二：第一次将本地项目上传到 GitHub

```bash
cd project
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:USERNAME/REPOSITORY.git
git push -u origin main
```

HTTPS：

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git push -u origin main
```

### 场景三：在新分支开发

```bash
git switch main
git pull --rebase origin main
git switch -c feature/new-feature

# 修改文件

git status
git add .
git commit -m "Add new feature"
git push -u origin feature/new-feature
```

### 场景四：本地有修改，但远程也有更新

```bash
git status
git stash -u
git pull --rebase
git stash pop
```

处理冲突后：

```bash
git add .
git commit -m "Resolve conflicts"
git push
```

### 场景五：提交后发现漏改文件

```bash
# 修改漏掉的文件
git add missing_file.py
git commit --amend --no-edit
```

未推送时直接继续。

已经推送时：

```bash
git push --force-with-lease
```

### 场景六：提交信息写错

```bash
git commit --amend -m "Correct commit message"
```

### 场景七：误提交大文件

如果尚未推送：

```bash
git rm --cached large_file.bin
echo "large_file.bin" >> .gitignore
git add .gitignore
git commit --amend --no-edit
```

### 场景八：放弃当前所有未提交修改

```bash
git restore .
git clean -fd
```

其中：

```bash
git restore .
```

删除已跟踪文件的修改。

```bash
git clean -fd
```

删除未跟踪文件和目录。

执行前先预览：

```bash
git clean -fdn
```

### 场景九：将本地分支完全重置为远程分支

```bash
git fetch origin
git reset --hard origin/main
git clean -fd
```

该操作会删除本地未提交修改和未跟踪文件，应谨慎执行。

---

## 28. 常见报错与处理

### 28.1 `fatal: not a git repository`

当前目录不是 Git 仓库。

检查目录：

```bash
pwd
ls -la
```

进入正确仓库：

```bash
cd path/to/repository
```

确认存在：

```bash
ls -la .git
```

如果确实是新项目：

```bash
git init
```

---

### 28.2 `nothing to commit, working tree clean`

当前没有未提交修改。

检查：

```bash
git status
```

如果文件未被跟踪：

```bash
git add .
git commit -m "Add files"
```

如果文件被 `.gitignore` 忽略：

```bash
git check-ignore -v file_name
```

---

### 28.3 `src refspec main does not match any`

通常是本地还没有提交，或当前分支不叫 `main`。

检查：

```bash
git branch
git log --oneline
```

如果还没有提交：

```bash
git add .
git commit -m "Initial commit"
```

将分支改为 `main`：

```bash
git branch -M main
git push -u origin main
```

---

### 28.4 `remote origin already exists`

查看已有远程仓库：

```bash
git remote -v
```

修改地址：

```bash
git remote set-url origin NEW_URL
```

或者删除后重新添加：

```bash
git remote remove origin
git remote add origin NEW_URL
```

---

### 28.5 `rejected non-fast-forward`

远程分支包含本地没有的提交。

推荐：

```bash
git pull --rebase origin main
git push origin main
```

如果发生冲突：

```bash
git status
# 修改冲突文件
git add .
git rebase --continue
git push
```

不要未经确认直接强制推送。

---

### 28.6 `Your branch is ahead of origin/main`

本地有尚未推送的提交。

```bash
git push
```

---

### 28.7 `Your branch is behind origin/main`

远程有新的提交。

```bash
git pull --rebase
```

---

### 28.8 `Your branch and origin/main have diverged`

本地和远程均有不同提交。

优先使用：

```bash
git pull --rebase origin main
```

解决冲突后：

```bash
git add .
git rebase --continue
git push
```

---

### 28.9 `Please commit your changes or stash them before you merge`

当前有未提交修改。

选择提交：

```bash
git add .
git commit -m "Save local changes"
git pull
```

或者暂存：

```bash
git stash -u
git pull
git stash pop
```

---

### 28.10 `Permission denied (publickey)`

SSH 密钥未配置、未添加到 GitHub，或 SSH Agent 未加载密钥。

检查远程地址：

```bash
git remote -v
```

测试 GitHub SSH：

```bash
ssh -T git@github.com
```

查看本地密钥：

```bash
ls -la ~/.ssh
```

启动 Agent 并添加密钥：

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

也可以临时改用 HTTPS：

```bash
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

---

### 28.11 HTTPS 登录失败

GitHub 不接受账户密码作为 Git HTTPS 推送密码。应使用：

- Personal Access Token
- GitHub CLI 登录
- SSH 密钥

使用 GitHub CLI：

```bash
gh auth login
```

---

### 28.12 `detached HEAD`

当前位于某个提交或标签，而不是正常分支。

查看：

```bash
git status
```

回到已有分支：

```bash
git switch main
```

如果当前修改需要保留：

```bash
git switch -c recovery_branch
```

---

### 28.13 `cannot lock ref` 或锁文件错误

确认没有其他 Git 进程正在运行：

```bash
ps aux | grep git
```

检查锁文件：

```bash
find .git -name "*.lock"
```

确认没有 Git 进程后，才可删除对应锁文件，例如：

```bash
rm -f .git/index.lock
```

---

### 28.14 大文件超过 GitHub 限制

查看大文件：

```bash
find . -type f -size +50M
```

如果尚未提交：

```bash
git rm --cached path/to/large_file
echo "path/to/large_file" >> .gitignore
git add .gitignore
git commit
```

模型权重、数据集和大规模日志不建议直接存入普通 Git 仓库。可使用 Git LFS 或外部存储。

---

### 28.15 子模块为空或未下载

```bash
git submodule update --init --recursive
```

更新子模块：

```bash
git submodule update --remote --recursive
```

克隆时自动下载：

```bash
git clone --recurse-submodules REPOSITORY_URL
```

---

## 29. Git LFS 常用命令

安装并初始化：

```bash
git lfs install
```

跟踪特定类型文件：

```bash
git lfs track "*.pth"
git lfs track "*.ckpt"
git lfs track "*.zip"
```

查看跟踪规则：

```bash
cat .gitattributes
```

提交规则：

```bash
git add .gitattributes
git add model.pth
git commit -m "Track model weights with Git LFS"
git push
```

查看 LFS 文件：

```bash
git lfs ls-files
```

拉取 LFS 文件：

```bash
git lfs pull
```

---

## 30. 清理本地仓库

### 查看会被删除的未跟踪文件

```bash
git clean -n
```

### 查看会被删除的未跟踪文件和目录

```bash
git clean -fdn
```

### 删除未跟踪文件

```bash
git clean -f
```

### 删除未跟踪文件和目录

```bash
git clean -fd
```

### 删除被 `.gitignore` 忽略的文件

预览：

```bash
git clean -fdXn
```

执行：

```bash
git clean -fdX
```

### 清理失效的远程分支引用

```bash
git fetch --prune
```

或者：

```bash
git remote prune origin
```

---

## 31. 常用别名

设置简洁状态：

```bash
git config --global alias.st "status -s"
```

设置图形化日志：

```bash
git config --global alias.lg "log --oneline --graph --decorate --all"
```

设置提交：

```bash
git config --global alias.cm "commit -m"
```

设置当前分支：

```bash
git config --global alias.br "branch"
```

设置切换分支：

```bash
git config --global alias.sw "switch"
```

使用：

```bash
git st
git lg
git cm "Update client"
git br
git sw main
```

---

## 32. 推荐提交信息格式

简洁写法：

```text
Add PiperX hardware client
Fix CAN connection retry
Update installation guide
Remove obsolete joint limit
Refactor policy inference loop
Document deployment steps
```

常见动词：

```text
Add
Fix
Update
Remove
Refactor
Rename
Document
Test
Improve
Revert
```

可采用类型前缀：

```text
feat: add PiperX client
fix: correct joint feedback parsing
docs: update deployment guide
refactor: simplify control loop
test: add CAN communication test
chore: update dependencies
```

---

## 33. 每日最常用命令速查

### 查看状态

```bash
git status
```

### 查看修改

```bash
git diff
```

### 暂存全部修改

```bash
git add .
```

### 提交

```bash
git commit -m "Describe changes"
```

### 拉取远程更新

```bash
git pull --rebase
```

### 推送

```bash
git push
```

### 查看日志

```bash
git log --oneline --graph --decorate --all
```

### 创建并切换分支

```bash
git switch -c branch_name
```

### 切换到主分支

```bash
git switch main
```

### 暂存未提交修改

```bash
git stash -u
```

### 恢复暂存修改

```bash
git stash pop
```

### 取消暂存

```bash
git restore --staged file.py
```

### 放弃文件修改

```bash
git restore file.py
```

### 撤销最近一次提交但保留修改

```bash
git reset --soft HEAD~1
```

### 安全强制推送

```bash
git push --force-with-lease
```

---

## 34. 推荐日常工作流

```bash
# 1. 进入仓库
cd project

# 2. 查看状态
git status

# 3. 同步远程分支
git pull --rebase

# 4. 修改文件

# 5. 查看修改
git diff

# 6. 暂存修改
git add .

# 7. 检查即将提交的内容
git diff --staged

# 8. 提交
git commit -m "Describe changes"

# 9. 推送
git push
```

在功能分支中开发：

```bash
git switch main
git pull --rebase origin main
git switch -c feature/feature-name

# 修改和测试

git add .
git commit -m "Add feature"
git push -u origin feature/feature-name
```

---

## 35. 危险命令清单

以下命令可能覆盖或永久删除本地修改，执行前应先运行 `git status`，必要时使用 `git stash -u` 或创建备份分支。

```bash
git reset --hard
git reset --hard COMMIT_HASH
git clean -fd
git clean -fdX
git push --force
git branch -D branch_name
git restore .
```

相对安全的替代方法：

```bash
git push --force-with-lease
git revert COMMIT_HASH
git stash -u
git switch -c backup_branch
```
