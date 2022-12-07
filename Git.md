# Git

## Git 是什么

Git 是目前世界上最先进的分布式版本控制系统，支持 https 和 ssh 协议，ssh 协议最快。

## 版本库

又称仓库，repository，这里的所有文件都被 git 管理，每个文件的修改、删除，git 都能追踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

## Git 使用

- 配置用户名和邮箱
    - git config --global user.name "用户名"
    - git config --global user.email "邮箱"
- 克隆项目
    - git clone "项目路径"
- 管理项目
    - git init
- 提交项目
    - 提交所有的文件 git add .
    - git add "文件名"
    - git commit -m "备注"
    - 二次提交 git commit --amend --no-edit
- 查看历史
    - git log
- 回到上次提交版本
    - git checkout HEAD "文件名"

``` text
- git status    查看仓库当前的状态，有哪些需要add和commit
- git reset --hard HEAD^    回到上个版本
- git checkout -b "分支名"    创建并切换分支，相当于git branch dev，git checkout dev
- git branch    查看所有分支，当前分支前面以*标注
- git branch -d <name>    删除分支，操作后未合并不能删除
- git pull    抓取
- git config --global alias.<alias-name> <git-command>    配置一个git命令的快捷方式
- git push    推送至远程库
      -f 二次提交需要加
```

## Git 提交理解

工作区 add -> 暂存区 commit -> 本地库 push -> 远程库

## Code Review 流程

- git add "文件名"
- git commit -m "评论"
- git push

- 提交者发起 topic 分支到目标分支（日常开发一般是 develop）的 Merge Request（以下简称 MR），assign 给 peer（你的同级同事，一般不要直接给 Lead 或项目维护者） 做 review。
    - 代码变动要尽量小且专注于一个任务，不要攒的很大，或者做多个任务，要保证审查者可以较快、较容易的 review。需要一次性提交大量不需要 review 的文件的（比如框架、依赖包等），分两个 commit，不需要 review 的放在第一个 commit，并在 MR 描述中说明。
    - 如果与目标分支有冲突，提交者应该自己使用 git rebase 或 git merge（共享分支的情况）解决。
    - Assign 给别人之前一定要自己先 review 一遍（在 GitLab 上检查最终效果），确保自己提交的每一行变更都是正确的、必要的，对自己的代码负责，不要浪费别人的时间。
- 审查者 review 代码。
    - 对 Markdown 中各项要求进行检查，在任何有疑问或建议的地方留评论。
    - 如果提交者已针对之前的评论做了修复，审查者需在确认问题已修复后 resolve thread（解决话题）。
    - 从中学习一些好的东西。
    - Review 完后，assign 给提交者处理。
- 提交者响应评论。
    - 确实有问题的，修复之，注意举一反三，检查其它地方是否有类似问题，一并修改。如果该分支未被其他人使用，应使用 git commit --amend 提交以减少不必要的 commit 历史（--amend 选项表示修改上一个 commit 而不是创建一个新的 commit，commit 被修改过后，git push 必须加 -f 强制推送才能 push 成功）。
    - 不同意的，讨论。
    - 完成后，assign 给审查者再次 review（不需要额外留评论说修好了，assign 回去就表示修好了）。回到第二步。
- 审查者确认没有问题之后，将 MR assign 给 Lead 或项目维护者进行二次 review 和合并。

Git 的使用和 MR 的流程要对着要点进行检查，确保不会做错。
