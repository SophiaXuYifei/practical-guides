# Nano 使用指南

`nano` 是 Linux/Unix 系统中常见的终端文本编辑器，适合快速修改配置文件、脚本、Markdown 文档和代码文件。它不需要记忆复杂的编辑模式，打开文件后即可直接输入和修改。

---

## 1. 打开或创建文件

### 打开已有文件

```bash
nano 文件名
```

例如：

```bash
nano README.md
nano config.yaml
nano test.py
```

### 创建新文件

当指定的文件不存在时，`nano` 会创建一个新文件：

```bash
nano notes.md
```

编辑后保存，文件才会真正写入磁盘。

### 打开指定目录中的文件

```bash
nano ~/openpi/README.md
nano /home/sophia/project/config.yaml
```

其中：

- `~` 表示当前用户的主目录，例如 `/home/sophia`
- `.` 表示当前目录
- `..` 表示上一级目录

---

## 2. Nano 界面说明

打开文件后，界面主要分为三部分：

1. 顶部：显示 Nano 版本和当前文件名。
2. 中间：文件内容编辑区。
3. 底部：常用快捷键提示。

底部快捷键中的符号含义：

- `^` 表示 `Ctrl`
- `M-` 表示 `Alt`，部分终端也可先按 `Esc`，松开后再按对应键

例如：

```text
^O Write Out
```

表示按：

```text
Ctrl + O
```

---

## 3. 最基本的编辑流程

打开文件：

```bash
nano test.txt
```

直接使用键盘输入或修改内容。

保存文件：

```text
Ctrl + O
```

Nano 会在底部显示文件名：

```text
File Name to Write: test.txt
```

按 `Enter` 确认。

退出 Nano：

```text
Ctrl + X
```

完整流程：

```text
nano test.txt
输入或修改内容
Ctrl + O
Enter
Ctrl + X
```

---

## 4. 保存与退出

### 保存当前文件

```text
Ctrl + O
```

然后按：

```text
Enter
```

### 退出 Nano

```text
Ctrl + X
```

如果文件已修改但未保存，Nano 会询问：

```text
Save modified buffer?
```

常用选择：

- `Y`：保存后退出
- `N`：不保存，直接退出
- `Ctrl + C`：取消退出，返回编辑界面

选择 `Y` 后，需要再次按 `Enter` 确认文件名。

### 另存为其他文件

按：

```text
Ctrl + O
```

将底部的文件名改为新文件名，再按 `Enter`。

例如，将 `config.yaml` 另存为：

```text
config_backup.yaml
```

---

## 5. 光标移动

Nano 支持方向键直接移动。

| 操作 | 快捷键 |
|---|---|
| 向左移动一个字符 | `Left` 或 `Ctrl + B` |
| 向右移动一个字符 | `Right` 或 `Ctrl + F` |
| 向上移动一行 | `Up` 或 `Ctrl + P` |
| 向下移动一行 | `Down` 或 `Ctrl + N` |
| 移动到当前行开头 | `Ctrl + A` |
| 移动到当前行末尾 | `Ctrl + E` |
| 向上翻页 | `Ctrl + Y` |
| 向下翻页 | `Ctrl + V` |
| 移动到文件开头 | `Alt + \` |
| 移动到文件末尾 | `Alt + /` |

---

## 6. 跳转到指定行

按：

```text
Ctrl + _
```

部分键盘需要按：

```text
Ctrl + Shift + -
```

输入行号后按 `Enter`。

例如，跳转到第 120 行：

```text
120
```

也可以输入行号和列号：

```text
120,15
```

表示跳转到第 120 行、第 15 列。

---

## 7. 显示行号

### 临时显示行号

启动 Nano 时添加 `-l`：

```bash
nano -l test.py
```

### 在 Nano 内切换行号显示

```text
Alt + Shift + 3
```

部分终端中对应：

```text
Alt + #
```

### 永久开启行号

编辑 Nano 配置文件：

```bash
nano ~/.nanorc
```

加入：

```text
set linenumbers
```

保存后重新打开 Nano。

---

## 8. 搜索文本

按：

```text
Ctrl + W
```

输入要搜索的内容，再按 `Enter`。

例如搜索：

```text
joint_limit
```

继续查找下一个匹配项：

```text
Alt + W
```

搜索时通常区分大小写的行为取决于 Nano 配置和当前选项。可在搜索界面查看底部提示并切换相关选项。

---

## 9. 搜索并替换

按：

```text
Ctrl + \
```

输入要查找的文本，按 `Enter`。

然后输入替换后的文本，再按 `Enter`。

Nano 会逐个询问是否替换：

- `Y`：替换当前匹配项
- `N`：跳过当前匹配项
- `A`：替换全部匹配项
- `Ctrl + C`：取消替换

例如，将：

```text
localhost
```

替换为：

```text
127.0.0.1
```

---

## 10. 删除、剪切、复制和粘贴

### 删除字符

| 操作 | 快捷键 |
|---|---|
| 删除光标左侧字符 | `Backspace` |
| 删除光标位置字符 | `Delete` 或 `Ctrl + D` |

### 剪切当前行

```text
Ctrl + K
```

如果没有选中文本，`Ctrl + K` 会剪切当前整行。

连续按多次可以剪切多行。

### 粘贴 Nano 剪切板内容

```text
Ctrl + U
```

### 复制当前行

Nano 没有单独的“复制当前行”快捷键，可使用以下方法：

1. 按 `Ctrl + K` 剪切当前行。
2. 按 `Ctrl + U` 粘贴恢复当前行。
3. 再按一次 `Ctrl + U`，复制出第二份。

---

## 11. 选择一段文本

将光标移动到选区起点，按：

```text
Alt + A
```

部分终端可使用：

```text
Ctrl + 6
```

然后移动光标，选中目标文本。

选中后：

- 剪切：`Ctrl + K`
- 复制：`Alt + 6`
- 粘贴：`Ctrl + U`

取消选择：

```text
Alt + A
```

---

## 12. 撤销与重做

### 撤销

```text
Alt + U
```

### 重做

```text
Alt + E
```

某些终端会占用 `Alt` 快捷键，此时可先按 `Esc`，松开后再按对应字母。

---

## 13. 插入其他文件内容

在当前光标位置插入另一个文件的内容：

```text
Ctrl + R
```

输入文件路径并按 `Enter`。

例如：

```text
/home/sophia/template.yaml
```

该操作不会切换到另一个文件，而是将目标文件的内容插入当前文件。

---

## 14. 查看帮助

按：

```text
Ctrl + G
```

进入 Nano 帮助页面。

退出帮助页面：

```text
Ctrl + X
```

Nano 底部显示的快捷键会根据当前操作界面变化，因此遇到不确定的操作时，应先查看底部提示。

---

## 15. 编辑需要管理员权限的文件

部分系统配置文件普通用户无法直接保存，例如：

```bash
nano /etc/hosts
```

可能出现：

```text
Permission denied
```

应使用：

```bash
sudo nano /etc/hosts
```

其他常见示例：

```bash
sudo nano /etc/fstab
sudo nano /etc/ssh/sshd_config
sudo nano /etc/systemd/system/my-service.service
```

编辑系统配置文件前，建议先备份：

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo nano /etc/ssh/sshd_config
```

不要对普通用户目录中的文件随意使用 `sudo nano`，否则文件可能被保存为 `root` 所有，导致之后普通用户无法修改。

---

## 16. 文件权限问题

查看文件权限：

```bash
ls -l 文件名
```

例如：

```bash
ls -l config.yaml
```

如果文件属于 `root`：

```text
-rw-r--r-- 1 root root ...
```

可将文件所有者改回当前用户：

```bash
sudo chown "$USER":"$USER" config.yaml
```

对于指定用户 `sophia`：

```bash
sudo chown sophia:sophia config.yaml
```

---

## 17. 常用启动参数

### 显示行号

```bash
nano -l test.py
```

### 禁止自动换行

```bash
nano -w config.yaml
```

编辑 YAML、Python、Shell 脚本和代码文件时，推荐使用 `-w`，避免 Nano 对长行进行自动换行。

### 创建备份文件

```bash
nano -B config.yaml
```

保存时会生成备份文件，例如：

```text
config.yaml~
```

### 使用鼠标

```bash
nano -m test.txt
```

在支持鼠标事件的终端中，可以使用鼠标定位光标。

### 同时使用多个参数

```bash
nano -l -w -B config.yaml
```

也可以写成：

```bash
nano -lwB config.yaml
```

---

## 18. 配置 `~/.nanorc`

Nano 的用户配置文件是：

```text
~/.nanorc
```

打开配置文件：

```bash
nano ~/.nanorc
```

推荐配置：

```text
set linenumbers
set tabsize 4
set tabstospaces
set autoindent
set mouse
set minibar
set stateflags
set backup
```

配置含义：

| 配置 | 作用 |
|---|---|
| `set linenumbers` | 显示行号 |
| `set tabsize 4` | Tab 宽度设为 4 个字符 |
| `set tabstospaces` | 将 Tab 转换为空格 |
| `set autoindent` | 新行继承上一行缩进 |
| `set mouse` | 启用鼠标 |
| `set minibar` | 使用较紧凑的状态栏 |
| `set stateflags` | 显示文件状态 |
| `set backup` | 保存时创建备份 |

修改配置后，重新启动 Nano 生效。

如果某个选项在当前 Nano 版本中不受支持，启动时会显示配置错误。删除对应配置行即可。

---

## 19. 编辑 YAML 文件时的注意事项

YAML 对缩进非常敏感。编辑 YAML 时建议使用：

```bash
nano -lw config.yaml
```

建议在 `~/.nanorc` 中设置：

```text
set tabsize 2
set tabstospaces
set autoindent
```

注意：

- YAML 缩进应使用空格，不要使用 Tab。
- 同一层级必须保持相同缩进。
- 冒号后通常需要一个空格。
- 不要随意改变列表项 `-` 的缩进。

示例：

```yaml
server:
  host: 127.0.0.1
  port: 8000

tasks:
  - pick
  - place
```

---

## 20. 编辑 Python 文件时的注意事项

推荐命令：

```bash
nano -lw script.py
```

推荐配置：

```text
set tabsize 4
set tabstospaces
set autoindent
set linenumbers
```

Python 使用缩进表示代码结构，因此不要混用 Tab 和空格。

编辑完成后可检查语法：

```bash
python -m py_compile script.py
```

运行文件：

```bash
python script.py
```

---

## 21. 编辑 Shell 脚本

创建脚本：

```bash
nano run.sh
```

示例内容：

```bash
#!/usr/bin/env bash

set -e

echo "Starting program..."
python main.py
```

保存并退出后，添加执行权限：

```bash
chmod +x run.sh
```

运行：

```bash
./run.sh
```

也可以直接使用：

```bash
bash run.sh
```

---

## 22. 编辑 Git 提交信息

Git 有时会自动调用默认编辑器输入提交信息。

若希望将 Nano 设置为 Git 默认编辑器：

```bash
git config --global core.editor "nano"
```

之后执行：

```bash
git commit
```

会进入 Nano。

填写提交信息后：

```text
Ctrl + O
Enter
Ctrl + X
```

查看当前 Git 编辑器配置：

```bash
git config --global core.editor
```

---

## 23. 将 Nano 设置为系统默认终端编辑器

当前终端会话中设置：

```bash
export EDITOR=nano
export VISUAL=nano
```

永久设置可写入 `~/.bashrc`：

```bash
nano ~/.bashrc
```

在文件末尾添加：

```bash
export EDITOR=nano
export VISUAL=nano
```

保存后执行：

```bash
source ~/.bashrc
```

---

## 24. 终端复制与粘贴

Nano 自身的剪切板与系统剪切板不同。

### Nano 内部剪切板

- 剪切：`Ctrl + K`
- 粘贴：`Ctrl + U`
- 复制选区：`Alt + 6`

### 系统剪切板

在常见 Linux 终端中：

- 复制：`Ctrl + Shift + C`
- 粘贴：`Ctrl + Shift + V`

在 macOS Terminal 或 iTerm2 中：

- 复制：`Command + C`
- 粘贴：`Command + V`

通过 SSH 使用 Nano 时，系统剪切板由本地终端管理，而 Nano 的 `Ctrl + K`、`Ctrl + U` 只作用于 Nano 内部。

---

## 25. 常见操作场景

### 场景一：快速修改配置文件

```bash
nano -lw config.yaml
```

修改后：

```text
Ctrl + O
Enter
Ctrl + X
```

### 场景二：修改系统配置

```bash
sudo cp /etc/hosts /etc/hosts.bak
sudo nano /etc/hosts
```

### 场景三：跳转到报错行

假设 Python 报错显示：

```text
File "main.py", line 128
```

打开文件：

```bash
nano -l main.py
```

按：

```text
Ctrl + _
```

输入：

```text
128
```

按 `Enter`。

### 场景四：查找变量名

```text
Ctrl + W
```

输入：

```text
joint_limit
```

按 `Enter`。

查找下一个：

```text
Alt + W
```

### 场景五：批量替换变量名

```text
Ctrl + \
```

输入旧变量名，按 `Enter`；输入新变量名，再按 `Enter`；按 `A` 替换全部。

### 场景六：放弃所有修改

按：

```text
Ctrl + X
```

当询问是否保存时按：

```text
N
```

---

## 26. 常见问题

### 26.1 按 `Ctrl + X` 后无法退出

文件可能有未保存修改。底部会显示：

```text
Save modified buffer?
```

选择：

- `Y`：保存
- `N`：不保存
- `Ctrl + C`：取消退出

### 26.2 保存时显示 `Permission denied`

当前用户没有写权限。

如果是系统文件：

```bash
sudo nano 文件路径
```

如果是自己目录中的文件，先检查所有者：

```bash
ls -l 文件名
```

必要时修正：

```bash
sudo chown "$USER":"$USER" 文件名
```

### 26.3 快捷键中的 `Alt` 无效

部分终端会拦截 `Alt` 组合键。可尝试：

1. 先按 `Esc`
2. 松开 `Esc`
3. 再按对应字母

例如 `Alt + U` 可尝试：

```text
Esc
U
```

### 26.4 粘贴后格式混乱

可能原因包括：

- 终端自动缩进
- 粘贴内容中包含 Tab
- YAML 缩进不一致
- 长行被终端视觉换行

编辑代码和配置文件时建议：

```bash
nano -lw 文件名
```

### 26.5 Nano 提示文件正在被编辑

Nano 可能检测到锁文件，或该文件确实被另一个进程打开。

先确认是否有其他 Nano 进程：

```bash
ps aux | grep nano
```

不要在确认前强制覆盖，以免丢失另一编辑会话中的修改。

### 26.6 文件打开后内容只读

可能是权限不足，或 Nano 以只读模式启动。

检查权限：

```bash
ls -l 文件名
```

使用管理员权限重新打开：

```bash
sudo nano 文件名
```

---

## 27. 推荐工作习惯

1. 修改重要配置文件前先备份。
2. 编辑代码和 YAML 时使用 `nano -lw`。
3. 保存后再退出，不要仅依赖退出时的保存提示。
4. 使用 `nano -l` 显示行号，便于定位报错。
5. 避免对用户目录文件使用 `sudo nano`。
6. 修改系统服务或 SSH 配置后，先做语法检查，再重启服务。
7. 大规模代码修改优先使用 VS Code；Nano 更适合快速修复和服务器端临时编辑。

---

## 28. 常用快捷键速查表

| 功能 | 快捷键 |
|---|---|
| 保存 | `Ctrl + O` |
| 退出 | `Ctrl + X` |
| 帮助 | `Ctrl + G` |
| 搜索 | `Ctrl + W` |
| 搜索下一个 | `Alt + W` |
| 搜索替换 | `Ctrl + \` |
| 跳转到行 | `Ctrl + _` |
| 剪切当前行或选区 | `Ctrl + K` |
| 粘贴 | `Ctrl + U` |
| 开始或结束选择 | `Alt + A` |
| 复制选区 | `Alt + 6` |
| 撤销 | `Alt + U` |
| 重做 | `Alt + E` |
| 移动到行首 | `Ctrl + A` |
| 移动到行尾 | `Ctrl + E` |
| 向上翻页 | `Ctrl + Y` |
| 向下翻页 | `Ctrl + V` |
| 文件开头 | `Alt + \` |
| 文件末尾 | `Alt + /` |
| 插入其他文件 | `Ctrl + R` |
| 显示或隐藏行号 | `Alt + #` |

---

## 29. 最常用命令汇总

```bash
# 打开文件
nano file.txt

# 显示行号
nano -l file.txt

# 禁止自动换行
nano -w file.txt

# 显示行号并禁止自动换行
nano -lw file.txt

# 编辑系统文件
sudo nano /etc/hosts

# 编辑 Nano 配置
nano ~/.nanorc

# 将 Nano 设置为 Git 默认编辑器
git config --global core.editor "nano"

# 将 Nano 设置为当前终端默认编辑器
export EDITOR=nano
export VISUAL=nano
```
