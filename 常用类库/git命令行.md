#### 创建合并分支

**创建并切换分支**	`git checkout -b dev`

**查看本地分支**  `git branch`

**查看远程所有分支**	`git branch -r`

**查看远程及本地所有分支**	`git branch -a`

**同步所有分支**	`git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done`

**本地所有分支与远程保持同步**	`git fetch --all`

**拉取所有分支代码** `git pull --all`

**切换分支**	`git checkout name`

**合并某分支到当前分支**：`git merge name`

**删除分支**：`git branch –d name`

