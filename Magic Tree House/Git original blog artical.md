首先我们必须承认，备份老版本的文件对自己是非常有利的。


第二种方法，可以利用系统自带的工具来进行自动地比较检索。
我们可以使用工具帮助我们检测文件之间的区别







第二课：

使用ls -a可以查看所有文件，包括隐藏的系统文件。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgm9fcxlywj20gj092gly.jpg)

git status
通过它可以看到上次commit后哪些文件已经被更改。

git会使用一个称为staging area的临时区域，每次可以往里添加一个文件。都添加完后，在我准备commit时，git将存储区域中的全部内容绑定到单一的commit，然后添加到repository。

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgm8w5jftmj211g0jrak5.jpg)

可以使用git status来查看我先前已经添加的内容。


自我们上次再次查看概念图以来，我们引入了一些新概念。

git init （git 初始化）
git add （git 添加）
git status （git 状态）
staging area （暂存区）
working directory （工作目录）

git add 和git status都是在staging area工作，帮助你commit；git status还显示了工作目录下的内容。

在第 1 课快要结束时提供了适用于你的平台的“设置工作空间”视频，如果你遵循此视频中的说明，则在运行 git commit 时，所选的编辑器将会出现，让你可以编写提交信息。如果收到错误消息，则应尝试重温第 1 课中的说明，并确保正确设置了文本编辑器。


你也可以通过命令行指定提交信息，即运行 git commit -m "Commit message"，而不是 git commit。设置编辑器仍然是一种好的做法，因为这可让你更轻松地编写较长的提交信息，以全面说明所做的更改。

运行git commit，Git打开我配置好的编辑器，使我能够编写commit消息。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgmbhqwolhj20yt0ezwg9.jpg)
标准git的惯例是，像下达命令一样撰写你的commit消息。
在弹出的编辑器中写完commit消息后，保存关闭即可。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgmbzlnkrhj20i50ex3yz.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgmbot19k4j20gf033jrc.jpg)
用git status查看，发现最初的那个initial commit消失了。并且指示了剩下的未追踪的文件。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgmbs0s6qdj20gd092gly.jpg)
所有文件更改commit后
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgmc272nejj20gc08rmxg.jpg)

git commit之前，可以用git status看看staging area里还有什么内容。什么是即将change to be committed，然后再写commit消息。

场景：有时候我修改保存完文件后，尚未add，就去吃饭了，休息了，忘了commit。回来不记得之前更改啥了。
更改index.js：

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgoenxu198j20gb05laa8.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgodagmepbj20i60evwfm.jpg)

git diff 不加任何参数，就可以对比工作目录（working directory）和staging area，这可以显示你所做的任何更改且未添加到staging area。

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgod04nl5wj20gk0chwey.jpg)
如果我把文件game.js里的变更添加到staging area，那么再次运行git diff，发现这次只能看到index.js的更改了。因为game.js在staging area和working directory里是一样的了。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgod6u1grvj20ij0it0tm.jpg)

如果要查看staging area和最近commit之间的不同，可以用
git diff --staged
有些工程师喜欢在commit前再次用该条指令检查下添加的文件是真的想要放入commit中的文件。
运行该指令后，只能看到game.js的更改，看不到index.html的更改，因为index.html依然是相同的。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgodikltj5j20l70kjt9v.jpg)
确认这个确实是我想要commit的内容后，就可以输入git commit
然后再输入git diff，发现只有index.html的内容了。因为这个还没有被commit

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgodomtkkzj20iv08djrn.jpg)
输入git diff --staged，看不到任何内容，因为刚刚commit了staging area的所有内容。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgodsdf2jcj20fx09eweu.jpg)
最后，我实际上不想要index.html中的这些更改，要取消的话，可以运行git reset --hard，放弃工作区或staging area的所有更改。运行的时候要小心，因为这部分内容没有被commit，所以一旦该语句执行后，是无法再被恢复的。运行后，再执行git diff，这时候就没有任何变更出现了。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgodz662d2j20fi0bk74t.jpg)


到目前为止，你做的每一个commit都是基于之前的commit，形成一个线性的commit历史记录。有时候你可能想对commit历史记录进行分枝产生多个版本。 如果你是要修复一个bug，加入一些新特性，或更新文档，一个直线型的变化是比较合理的。但如果你想要尝试一种你并不确定是否可行的新的实验性功能，却仍然想要一个可用的demo展示给前来询问的好友。或者也许你正在学习意大利语，想要制作一个面向意大利语用户的项目版本但又不能影响母语版本。在这种情况下你需要最终创建一个设置用于两种语言之间的切换。或许第一步你只是想要更改文本看看是否需要更改下布局。当然，你可以进行更改并记住所有commit的id，当你需要向人展示实际的正式版时用git checkout返回实际的正式版，然后再返回到其他版本。但如果你在实际版本中发现了一个bug需要修复，这时你又该怎么办呢？你需要更新记录，使用新的commit来作为实际版本。这样会比较复杂。为了轻松处理这种情形，git使你能够为你的commit创造新的标签。这些标签叫做分枝。
master分枝是大多数代码库中主要分枝的名称。每次创建代码库时，git都会为你创建一个master分枝。

之前的课中，当你checkout一些旧的commit时，会收到detached head消息。这种情况下，git是在警告你，你所看到的这个commit没有用分枝名称（branch name）进行标记。

我们可以按照之前checkout commit id的方式checkout分枝。只不过这次我们用的是人类能看懂的分枝名称，而不是之前读都读不通的一连串字符。如果你checkout一个分枝，然后进行commit，那么分枝标记会自动更新到新的commit上，而且该分枝也会保持checkout状态，你无需针对该分枝再次checkout。这也是为何你目前为止一直待在master分枝上直到这节课才知道分枝情况。

说到术语，我们有时候会将分枝中当前最后一个commit称为该分枝的尖端（tip）。单个commit上可能出现多个分枝标记，但是进行新的commit只会更新你checkout的分枝，其他分枝不受影响。

git branch
显示所有的分支，以及你当前所在的分支（后面带\*）
git branch +branch name
新建一个分支
git checkout +branch name
切换到某个分支


如果你和合作者同时在同一个分支上进行更改，你们就无法轻易地同时创建不同的功能。

大家共同开发一个项目的常见工作流程包括为每一个功能或bug修复创建新的分支。这样当多个人同时进行更改时，他们每个人都可以在休息后checkout他们的分支继续工作。不用担心某些内容出现变化。一旦某个功能或者bug修复完成后，相关作者可以更新master分支，使其指向新分支的顶端。或者master分支在此期间也出现了更改，可以使用gits和merge功能将其与当前master分支进行合并。

branch coins set up to track remote branch coins from origin.
remote branch意味着我自己并没有创建它。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgpou8an44j20fp01qa9x.jpg)

在git中，你可以使用命令git log --graph直观地查看分支结构
git log --graph --oneline master coins，--oneline让输出简短  查看master和coins两个分支
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgpore7uzij20f909qwf1.jpg)
查看master和easy-mode
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgpoxf3rq3j20g509tdgf.jpg)

git log怎么判断显示哪些commit给你呢？实际上，每个commit都知道它的父commit，换言之，它被创建时会存储一个引用，指向被checkout的commit（it stores a reference to the commit that was checked out when it was made.）如果当你位于一个分支上，你创建了一个commit，它依然会存储该分支顶点的commit id。commit不会关心任何分支名称。只有分支本身会存储分支的位置。log以当前commit或任何指定分支的最新commit为起点，一直往前追踪，直到达到没有父commit的commit。这通常是初始commit。

detached head
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgpqiar6h7j20s20dbdq1.jpg)

git checkout -b new\_branch\_name相当于运行两条命令：git branch new\_branch\_name和git checkout new\_branch\_name

git also has a record of what the code looked like before the two branches diverged.(git记录有两个分支分开前的代码状态)
当使用git合并commit后，会同时存储其两个父commit的信息

注意，我们在讨论删除分支时，意思是要删除标签，但是commit仍然存在于历史记录中。但是如果没有分支可以抵达这个commit，则删除分支可有效地放弃其commit。所以如果你在未合并前，就删除了coins分支，则基本上你放弃了这条branch上的所有commit，因为他们无法被抵达。
如果删除某个分支并导致无法从现有的分支访问一些提交，则在 Git 的垃圾收集过程运行之前，仍可继续通过提交 ID 访问这些提交。除非你主动关闭此过程，否则它将不时自动运行。也可以通过命令 git gc 手动运行此过程。
合并后，用git log查看的话，会列出所有合并的两条分支之前的commit，这些commit会以时间戳排序。因此可能会交错显示两分支的commit。但是这么一来也会带来一个副作用，这时查看git log的时候，因为commit是按照时间戳排列的，所以git log前后两个id未必是父子的关系。这个时候如果你想用git diff，就会看到这两个ID的不同，但这个意义不大。因为其中一个未必是在另一个的基础上修改的。
git show +commit id，通过该命令，你可以查看相对于其父commit，该commit中引入了哪些修改，而无需知道其父commit是哪一个。
git branch -d 分支名，他不会删除commit，仅仅只会删除标签。这会使得这部分commit难以查找。但是既然它们之前已经被合并到master了，所以可以通过master访问，也不是什么大问题。

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgs2xir2rxj20id05wdg1.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgs2yue5hdj20er02h3ye.jpg)

检测冲突
git just assumes that if you're merging together two commits that have changes in the same area,the authors will want to know about it and have the chance to figure out for themselves which change to keep.

自创建 easy-mode 分支以来，master 已经更新。在本例中，它增加了 coins 分支，而你可能想将其包含在 easy-mode 分支中。总的来说，如果你创建分支（进行试验或实现新特性），你希望定期将 master 合并到该分支，这是很常见的做法。这是因为，master 通常包含代码的正式版本，而且，希望试验性的更改包含所有对 master 的更改是很常见的想法。

git merge master easymode

merge conflict in game.js:这意味着这两个分支，主分支和easy-mode分支更改了game.js的同一部分。
要解决次冲突，我需要打开game.js，查找发生冲突的位置。git使用特殊行表示了冲突。因此我可以通过搜索行中的一堆小于号找到它。这些行将屏幕分成3个区域，顶部区域，标记为head是我的代码。底部区域，标记为master是当前位于主分支中的代码。中间部分，是已修改的两个分支的原始版本，git将其称为共同祖先。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgud8gg686j20im0khdhs.jpg)
处理冲突，修改后，保存关闭game.js
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgta7oitx2j20g00ki75b.jpg)
运行git status，显示both modified，这是因为两个分支修改了文件，由此产生了冲突。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgtaazpywcj20h008ugly.jpg)
运行git add game.js，再运行git status，显示冲突已修复。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgtalzwj5xj20i50grt9k.jpg)
运行git commit，终结merge
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgucv8js1uj20i90ezq3m.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgtarhppyvj20h70iuq3x.jpg)
运行git log -n 1， n意为number，即log中的第一个记录。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgtavofszaj20gf043wej.jpg)



每次通过命令行向 GitHub 发送更改时，都需要键入密码，以证明你有权修改版本库。这可能很快会让人觉得厌烦，因此，许多人都喜欢设置密码缓存，此功能让你只需键入密码一次，以后就会自动在该计算机上填写密码。要这样做，请按照此处的说明进行操作。如果使用 Windows 并在前面按照我们的 Git 安装说明进行操作，则你使用的是 msysgit，因此可以按照 msysgit 的说明进行操作。

working directory和staging area存在于每一个repository，但是由于GitHub repository托管在GitHub的服务器中，它们无法直接访问。
想象一下如果你的repository很大，有成百上千的commit，那么每次发送一个单一的commit，效率是很低的。

to allow for syncing data between two repositories,git has a concept of a remote repository. This lets you store the location of a repository that you will want to send and receive new commits to and from. Git users ofen refer to these remote repositories simply as remotes.
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgwgkqgtmsj210s0guqfs.jpg)
你可以通过remotes发送和接收的就是commit。但发送和接收数据最常见的方法不是选择每个单独的commit提交，而是指定分支提交。只要push分支，那么所有的commit都会被发送，因为它们都可以通过分支的顶端被触及（reachable）。如果其中某个commit在我们push分支前已经在github的服务器上，它是不会被发送的。

在github上新建一个repository。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgwekhlip9j20w90ggq43.jpg)
如果我在创建任何内容前在github创建一个repository，那么我可能会选中此方框。因为这样的话，我的repository开始时会有一个commit，你无法克隆没有commit的代码库，所以这样最好选择勾上这个框。但是我的repository中已经有我想要分享的commit，所以我不勾选。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgwem02uovj20si0h8t9p.jpg)

git remote  查看所有当前的远程代码库（remote）。
要将github上的代码库当做远程代码库，运行git remote add +任意名字 + URL
Now I can use any name here and it's the name that i'll use within this repository,to refer to the repository on Github.如果你只有一个远程代码库（remote），标准做法是将其命名为origin。

git remote -v  ：这里v指代verbose，冗长的意思。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgwhct4vm8j20gi093aao.jpg)
git push +remote name +local branch :发送我的更改到远程代码库。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgwhdikpe0j20s40bljt2.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgwhe9hxy5j20gi092dgi.jpg)

本课程假定学生将使用 HTTPS 而不是 SSH。请单击 HTTPS 按钮，然后复制为 HTTPS 显示的 URL。它将以 https:// 开头，而不是 git@github.com 开头。
如果对改为使用 SSH 有兴趣，可按照此处 的说明操作，但除非你已熟悉 SSH 密钥，否则不建议你这样做。

也可以直接在github网站上创建和编辑纯文本文件（plaintext）

当你在github里头更改或添加了新文件，或者有其他小伙伴上传或更改了文件，这时候github与你local的repository就不相同了。这时候，你可以用pull从github中同步你本地的repository。

git pull +remote name +pull branch
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxilr1hrhj20iw0k2t9s.jpg)

push pull针对的是branch，clone针对的是remote
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxiwgx22qj211r0kfqgl.jpg)

fork的真相，如果你不是fork，而是直接clone某人的repository，然后再在本地更改，然后再push到github，这样大家是不知道某人的贡献的，除非你刻意强调，并贴上他的链接。为了花更少的精力达到类似的效果，github提供了一个功能叫forking。通过forking你可以直接在github服务器上复制别人的repository，而不用先将代码拉取到本地计算机上。要做出修改的话，你可能先将代码拉取到本地计算机上，除非文件修改非常简单，你可以直接在github上修改的除外。forking和cloning很像，实际上fork是github在他们自己的机器上为你制作的clone。fork还有一些其他作用，比如github会持续跟踪记录有多少人fork你的repository，所有的fork都会链接回原代码库，并且更容易向原始repository建议更改。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxj3dd6vvj211y0kee3v.jpg)

克隆版本不需要知道原始repository，clone你fork的repository既可。

fork按钮
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxjq0udhrj211k0i1q4d.jpg)
实际上，当你clone repository的同时，git会自动设置一个remote指向你clone的repository。这时候就不必用git remote add了。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxkp89p1bj20gi092jry.jpg)
如果我想要某人能和我合作，她需要权限能够向该代码库push数据，需要把她添加到collaborator中。在settings中左侧边栏选择collaborators，然后添加她的github用户名即可。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxkz7t7oaj20s00ap0tr.jpg)

如果两个代码库都具有可以通过同一分支到达新的commit该怎么办？如果这种情况下push或pull会发生什么情况？
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxuy6ilj1j20s10g4jxk.jpg)


模拟 Sarah 的更改
在“辅助材料”部分中，有一个名为 sarah_changes.sh 的文件，它包含了代码，看起来像是 Sarah 修改了你在 GitHub 上的Fork。要运行此代码，请下载该文件，然后使用 Git Bash 或终端键入 cd，以切换到该文件的保存目录。然后，键入 bash sarah_changes.sh（后跟一个空格和Fork的 URL）。例如，如果 Caroline 要运行该代码，她将键入 bash sarah_changes.sh https://github.com/cbuckey-uda/recipes.git，但你应使用你的Fork而不是 Caroline 的Fork的 URL。如果你没有设置密码缓存，系统会提示你输入 GitHub 用户名和密码。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxv3kh72rj20r80ek40l.jpg)


实际上当你有一个remote setup的时候，git会将remote上的所有分支都在本地保存一个副本，这些副本会包含你最后一次push或pull时远程分支的状态
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh19onela1j20gb0gnmxz.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh19zosngpj211h0h8wpn.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1a2r2slwj211g0k87gw.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgxvnm9tddj21150jrtp5.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1bh5y9ygj211w0ki1dm.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1bjjonngj211t0kfati.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1auyytk5j20s50hqdif.jpg)
git fetch origin:更新remote origin的所有分支的本地副本。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1bc93f4bj20f90kj400.jpg)
git status
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1bmiq4pyj20cz05qglm.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1btv477pj20g90ibjs9.jpg)
git merge master origin/master
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1c0fr39nj20yo0ft0ux.jpg)
修改conflict
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1c3a8bo8j20i60fraaz.jpg)
git commit
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1c7qq2utj20yp0fognx.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1c9joqrjj20i60ftgmk.jpg)
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1cb7l0evj20g90c3js0.jpg)
git pull origin master
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1cdwqo22j20gc0fnwfm.jpg)
git push origin master
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fh1ckvuossj20gi0fqt9w.jpg)

既然git pull=git fetch+git merge，为什么之前一次的pull没有发生merge呢？原因是fast-forward merges。
这类merge发生于，当你合并两个commit，而这两个commit中的一个是另一个commit的祖先。
因为其中一个commit已经包含了另一个commit的历史信息了，所以去做merge这个事情本身并没有意义。只要把其中一个的label提前即可。
以下是一个例子：
http://lemonup.logdown.com/posts/166352-git-merge-fast-forward-difference

分享一个工作流，你可以在更新master前用来获取反馈。
1.首先在不同分支上进行本地更改
2.将该更改推送到我的fork
如果他人发现我的更改有问题，我就不至于打破我的master。
3.使用github上的pull request,让合作伙伴更容易看到我的更改内容，并进行评论。
4.我们都确认无误再合并到master

pull requests are not a feature of Git, they're a GitHub invention.
pull request意思是你让对方pull你的分支合并到你的主干上，目的是为了得到他人的审核。直接把它理解成merge request即可。

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltba5086j20gf0eoq3r.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltdbaqx1j20wg0fbjsq.jpg)
修改base fork的下拉菜单，选择你想要进行pull request的repository。这个千万不要搞错了搞成别人的库了。不过默认情况下，github认为是你要发送pull request给你fork的那个repository。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlte3yfs4j20l50hi75i.jpg)
选定base repository，在下面pull request的栏目里默认下就会加载你之前commit的message。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlteguclbj20rt0fnaba.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltf1t261j20ro0bjjsc.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltfufistj20io0hzjta.jpg)
点击commit f553c03，进入下面界面，可以查看commit所做修改，可以在右侧留下你的review结论。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltlyvu50j20rp0flwfs.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltnym4noj20ma0hggn4.jpg)

![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltrx3ewrj20hu0kjgn1.jpg)
修改拼写错误后，再push一次commit，就会发现commit的内容出现在之前的评论下方。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhltvbubo0j20lw0hxta5.jpg)

下面模拟当你发送pull request的同时，如果对方也发送了pull request，并且你们两人的更改有冲突的情况，该如何处理。

模拟 Sarah 的更改
要模拟 Sarah 的更改，请先从“辅助材料”部分中下载文件 sarah_changes_2.sh。然后，使用 Git Bash 或终端键入 cd，以切换到该文件的保存目录。接着，键入 bash sarah_changes_2.sh（后跟一个空格和Fork的 URL）。例如，如果 Caroline 要运行代码，她将键入 bash sarah_changes_2.sh https://github.com/cbuckey-uda/recipes.git，但你应使用你的Fork而不是 Caroline 的Fork的 URL。如果未设置密码缓存，则系统会提示你输入 GitHub 的用户名和密码。

此代码实际上并不创建拉取请求，而是更新 GitHub 上的提交历史记录，使其看似已合并了拉取请求。你无需合并拉取请求，而是需要在 GitHub 上的 master 分支中检查是否存在着含有信息“Merge pull request”的提交。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlvy1707oj20r509wdh4.jpg)
github上master的现状如下。模拟更新并合并成功。意即先review Sarah的commit，没有问题后，先合并到master。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlw1ijmvlj20r90d7aap.jpg)
拉取sarah修改后最新的master到本地
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlwhb9uv7j20fi05mt8t.jpg)
在本地合并master到分支different-oil
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlwq6hmy7j20gy0edt9l.jpg)
重新push different-oil分支到github
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlwsz038vj20eh03o0sr.jpg)
在github中，切换到different-oil分支查看
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlwz6c22sj20ru0fl75r.jpg)
点击view1，进入之前的pull request界面，可以看到pull request被更新，以及更新相关的commit。merge pull request按钮为绿色，说明没有发生冲突。
我估计，因为之前的这个merge pull request一直没有执行，所以在其执行前，所有的commit都会显示在该页面，表示是为了实现该merge pull request所做的commit。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlwxz958rj20l40fxabs.jpg)
我加入一个新的comment，提交后，新comment出现在如下位置。意即让我的合作伙伴再度检查一下。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlxe2xf92j20hi0fz3zs.jpg)
现在确认一切无误，可以按merge pull request按钮。按下后发现拉取请求的标题会默认自动沿用之前的信息，当然你可以根据需求更改。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlxm2rkc7j20ek0fytac.jpg)
点击confirm merge，显示如下。提示该分支可以删除。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlxp1w7t0j20lu0fvta2.jpg)
将github上该master分支重新pull回本地
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhlxvivbg7j20ge08zaal.jpg)
注意提交信息：

指出合并了拉取请求
提供了拉取请求的编号（在此为 #1）
指出了从哪个分支合并拉取请求（在此为 Chen-Isaac/different-oil）。
包含了拉取请求的标题。
每次合并拉取请求时，GitHub 都会自动创建类似上面的提交信息，以便你在提交历史记录中查看拉取请求。即使合并是快进合并，GitHub 仍会创建此提交。

fast-forward merge 会改变分枝指向的位置。它将分枝标记从一个commit挪到另一个commit。



注意：可以直接更改你的Fork中的 master 分支，但是，在协同构建公共版本库时，标准的做法是在Fork内的非 master 分支中进行更改。这样一来，可以轻松让你的 master 分支与原始版本库的 master 保持同步，并在准备好时将 master 中的更改合并到分支中。

Windows 用户请注意：随着故事的发展，它已经超出了 Windows 的路径长度限制。如果你在克隆时遇到错误，可以通过修改配置设置来解决它。请在 git bash 中运行此命令：git config --system core.longpaths true。

如有必要，更新拉取请求
如果某人合并你的拉取请求或发表评论，GitHub 会向你发送电子邮件并通知你。如果要求你进行一些更改，请将这些更改推送到你的Fork，以更新拉取请求。请确保让评审老师知道，他们应再看一次！

pull request发生冲突的解决方法。

从原始repository fork后，再clone到本地，在本地加一分枝，修改后push到fork的repository。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhnaj4w3uuj21ek0sykc2.jpg)
而恰巧此时，original的repository发生了变更。而且该变更和你的变更冲突。
冲突是无法在github上解决的，你只能在本地解决冲突。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhnansiutij21do0rwnkc.jpg)
此时你需要添加另一个远程代码库来将original repository的更改pull到本地。
之前指向你fork repository的远程代码库为origin，大多数人会将指向original代码库的远程代码库命名为upstream。
运行：git remote add upstream + 地址
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhnas6uavmj21eo0taav4.jpg)
接下来，在本地将master更新成upstream/master，
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhnau9gzgmj21du0s0ttw.jpg)
再在change分枝对更新后的master进行合并，处理冲突。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhnb2o2p3kj21ds0s27u4.jpg)
重新push master分枝和change分枝到fork的repository。（你无权push到original repository）其实无需push master的，但是这么做也许更好些。
这样会自动更新你的pull request请求。此时，你应该可以看的merge pull request的按钮变成绿色，冲突已经解决。
![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhnb4un4xuj21em0ru1kx.jpg)




