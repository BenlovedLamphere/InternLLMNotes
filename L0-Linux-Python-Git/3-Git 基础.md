```arduino
git config --global --get http.proxy
git config --global --get https.proxy
```

``` bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

```arduino
git config --global http.proxy http://proxyserver:port
git config --global https.proxy http://proxyserver:port
```

``` bash
git config --global -l
```



配置 git agent :

~/.ssh/config:

``` bash
Host github.com
    User git
    Hostname ssh.github.com
    Port 443
    ProxyCommand nc -X 5 -x 127.0.0.1:7890 %h %p
  	AddKeysToAgent yes
  	UseKeychain yes
  	IdentityFile ~/.ssh/id_ed25519

```

## **5. Git常用操作**



### **5.1 Git简易入门四部曲**



在Git入门当中我们只需要明白一下常用四个指令，即可轻松玩耍

对这四个指令我们可以称为 **"Git 经典四步曲"**

在Git的日常使用中，下面四步曲是常用的流程，尤其是在团队协作环境中。

- **添（Add）**
  - **命令**：`git add <文件名>` 或 `git add .`
  - **作用**：将修改过的文件添加到本地暂存区（Staging Area）。这一步是准备阶段，你可以选择性地添加文件，决定哪些修改应该被包括在即将进行的提交中。
- **提（Commit）**
  - **命令**：`git commit -m '描述信息'`
  - **作用**：将暂存区中的更改提交到本地仓库。这一步是将你的更改正式记录下来，每次提交都应附带一个清晰的描述信息，说明这次提交的目的或所解决的问题。
- **拉（Pull）**
  - **命令**：`git pull`
  - **作用**：从远程仓库拉取最新的内容到本地仓库，并自动尝试合并到当前分支。这一步是同步的重要环节，确保你的工作基于最新的项目状态进行。在多人协作中，定期拉取可以避免将来的合并冲突。
- **推（Push）**
  - **命令**：`git push`
  - **作用**：将本地仓库的更改推送到远程仓库。这一步是共享你的工作成果，让团队成员看到你的贡献。

帮助团队成员有效地管理和同步代码，避免工作冲突，确保项目的顺利进行。正确地使用这些命令可以极大地提高开发效率和协作质量。

### **5.2 Git其他指令**



**常用指令**

| 指令           | 描述                                       |
| -------------- | ------------------------------------------ |
| `git config`   | 配置用户信息和偏好设置                     |
| `git init`     | 初始化一个新的 Git 仓库                    |
| `git clone`    | 克隆一个远程仓库到本地                     |
| `git status`   | 查看仓库当前的状态，显示有变更的文件       |
| `git add`      | 将文件更改添加到暂存区                     |
| `git commit`   | 提交暂存区到仓库区                         |
| `git branch`   | 列出、创建或删除分支                       |
| `git checkout` | 切换分支或恢复工作树文件                   |
| `git merge`    | 合并两个或更多的开发历史                   |
| `git pull`     | 从另一仓库获取并合并本地的版本             |
| `git push`     | 更新远程引用和相关的对象                   |
| `git remote`   | 管理跟踪远程仓库的命令                     |
| `git fetch`    | 从远程仓库获取数据到本地仓库，但不自动合并 |

**进阶指令**

| 指令              | 描述                                                 |
| ----------------- | ---------------------------------------------------- |
| `git stash`       | 暂存当前工作目录的修改，以便可以切换分支             |
| `git cherry-pick` | 选择一个提交，将其作为新的提交引入                   |
| `git rebase`      | 将提交从一个分支移动到另一个分支                     |
| `git reset`       | 重设当前 HEAD 到指定状态，可选修改工作区和暂存区     |
| `git revert`      | 通过创建一个新的提交来撤销之前的提交                 |
| `git mv`          | 移动或重命名一个文件、目录或符号链接，并自动更新索引 |
| `git rm`          | 从工作区和索引中删除文件                             |

每个指令都有其特定的用途和场景，详细的使用方法和参数可以通过命令行的帮助文档（`git command -h`,例如 `git pull -h`）来获取更多信息。