
本文摘自[http://www.ruanyifeng.com/blog/2015/12/git-workflow.html][1]
更详细的信息参阅[https://www.15yan.com/story/6yueHxcgD9Z/][2], 翻译自 gitlab 官方文档.

[Gitlab flow][3] 是 Git flow 与 Github flow 的综合。它吸取了两者的优点，既有适应不同开发环境的弹性，又有单一主分支的简单和便利。它是 Gitlab.com 推荐的做法。

### 上游优先
Gitlab flow 的最大原则叫做"上游优先"（upsteam first），即只存在一个主分支master，它是所有其他分支的"上游"。只有上游分支采纳的代码变化，才能应用到其他分支。
[Chromium项目][4]就是一个例子，它明确规定，上游分支依次为：

- Linus Torvalds的分支
-  子系统（比如netdev）的分支
- 设备厂商（比如三星）的分支

### 持续发布
Gitlab flow 分成两种情况，适应不同的开发流程。
![][image-1]

对于"持续发布"的项目，它建议在master分支以外，再建立不同的环境分支。比如，"开发环境"的分支是master，"预发环境"的分支是pre-production，"生产环境"的分支是production。

开发分支是预发分支的"上游"，预发分支又是生产分支的"上游"。代码的变化，必须由"上游"向"下游"发展。比如，生产环境出现了bug，这时就要新建一个功能分支，先把它合并到master，确认没有问题，再cherry-pick到pre-production，这一步也没有问题，才进入production。

只有紧急情况，才允许跳过上游，直接合并到下游分支。

### 版本发布

![][image-2]

对于"版本发布"的项目，建议的做法是每一个稳定版本，都要从master分支拉出一个分支，比如2-3-stable、2-4-stable等等。

以后，只有修补bug，才允许将代码合并到这些分支，并且此时要更新小版本号。

五、一些小技巧

### Pull Request
![][image-3]

功能分支合并进master分支，必须通过Pull Request（Gitlab里面叫做 Merge Request）。
![][image-4]

前面说过，Pull Request本质是一种对话机制，你可以在提交的时候，@相关[人员][5]或[团队][6]，引起他们的注意。

### Protected branch

master分支应该受到保护，不是每个人都可以修改这个分支，以及拥有审批 Pull Request 的权力。

[Github][7] 和 [Gitlab][8] 都提供"保护分支"（Protected branch）这个功能。

### Issue

Issue 用于 Bug追踪和需求管理。建议先新建 
Issue，再新建对应的功能分支。功能分支总是为了解决一个或多个 Issue。

功能分支的名称，可以与issue的名字保持一致，并且以issue的编号起首，比如"15-require-a-password-to-change-it"。
![][image-5]

开发完成后，在提交说明里面，可以写上"fixes #14"或者"closes #67"。Github规定，只要commit message里面有下面这些[动词][9] + 编号，就会关闭对应的issue。

- close
- closes
- closed
- fix
- fixes
- fixed
- resolve
- resolves
- resolved

这种方式还可以一次关闭多个issue，或者关闭其他代码库的issue，格式是username/repository#issue\_number。

Pull Request被接受以后，issue关闭，原始分支就应该删除。如果以后该issue重新打开，新分支可以复用原来的名字。

### Merge节点

Git有两种合并：一种是"直进式合并"（fast forward），不生成单独的合并节点；另一种是"非直进式合并"（none fast-forword），会生成单独节点。

前者不利于保持commit信息的清晰，也不利于以后的回滚，建议总是采用后者（即使用--no-ff参数）。只要发生合并，就要有一个单独的合并节点。

### Squash 多个commit

为了便于他人阅读你的提交，也便于cherry-pick或撤销代码变化，在发起Pull Request之前，应该把多个commit合并成一个。（前提是，该分支只有你一个人开发，且没有跟master合并过。）

![][image-6]

[1]:	http://www.ruanyifeng.com/blog/2015/12/git-workflow.html
[2]:	https://www.15yan.com/story/6yueHxcgD9Z/
[3]:	http://doc.gitlab.com/ee/workflow/gitlab_flow.html
[4]:	https://www.chromium.org/chromium-os/chromiumos-design-docs/upstream-first
[5]:	https://github.com/blog/1004-mention-autocompletion
[6]:	https://github.com/blog/1121-introducing-team-mentions
[7]:	https://help.github.com/articles/about-protected-branches/
[8]:	http://doc.gitlab.com/ce/permissions/permissions.html
[9]:	https://help.github.com/articles/closing-issues-via-commit-messages/

[image-1]:	http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122306.png
[image-2]:	http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122307.png
[image-3]:	http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122310.png
[image-4]:	http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122308.png
[image-5]:	http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122311.png
[image-6]:	http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122309.png