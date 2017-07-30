###前言

使用Git和GitHub已经个把月了，基础的操作基本上都熟悉了。过程中也查阅了很多资料，其中优达学城的视频讲解估计是我目前见到的最系统的，下面我把这些基础的知识点做一下归纳总结，以供参考。

在具体的介绍之前，首先说一下Git和GitHub之间的区别。用一句简要的话来归纳，就是：**Git,itself,being the version control tool that Github is built on.**具体来说，Git是一个位于你计算机本地的版本控制工具，而GitHub则是基于Git构建的一个云端，那里是我们与他人分享与协作的一个场所。

###Git

我们先来了解一下Git这个版本控制工具。

在具体介绍Git的用法之前，我们先来考虑一下这么一个问题，为什么需要这么一个版本控制工具呢？引入版本控制工具有什么好处？版本工具有很多，Git和其他工具的差别又在哪里？

1. 版本控制工具的必要性

	首先，基于日常计算机的使用，我想我们很容易达成一个共识，那就是对工作作业过程中文件的老版本进行备份是非常必要的。因为我们很可能遇到这么一个问题，以编程举例，比如之前老版本的程序功能基本已经运作正常，在这个基础上新增一些功能，或者修复之前的某个bug，结果操作之后，新的一版软件出现了一些新的很奇怪的问题，bug没有找到，或者对这次修改或者新功能构建的逻辑不满意，希望重头来过。这个时候，我们会很希望可以回到本次作业之前的那个好的版本，再次进行操作。因此，早期我们在编程的时候，乃至于编辑word文档的时候，会经常在不同的阶段保存一个副本，这恐怕是最原始的版本管理方法了。
	
	由此可见，**恢复到之前某个特定版本的内容，是版本控制工具的核心诉求**。
	
2. 版本对照功能

	除了恢复到之前某个特定版本的内容，版本控制工具最好还应该具备不同版本之前的比较功能。
	
	让我们回到之前描述的那个场景，你之前编写的一个程序版本，运行成功了，但是当后来更新一版之后，你发现程序运行出现了bug。这个时候你会怎么办？如果在修改代码之前，你对老版本的程序有过备份，这时候可能绝大多数人的直觉反应，就是将程序更改前后的两份代码放在两个窗口中进行对比，用肉眼查看前后的更新点在哪里，考虑在这些更新点上是哪里出现了问题，对吧？如果你写的只是十来行代码的小程序，那么这种方法还算是可行的。但是如果你作业的代码是上千行乃至上万行，而且你版本上更改的地方又比较多，那这种查找bug的方式一定会让你崩溃。	
	这时候，如果有一个工具可以将两个版本的文件进行自动对比，标注其不同之处，那对于编程者查找bug而言真是一个福音。
	
	其实，我们的操作系统就已经自带了工具针对不同的文件进行比较检索。
	
	在windows系统下，可以在命令提示符（command prompt）中使用FC命令，来对不同的文件进行比较。FC，即是file compare的缩写。使用方法：利用cd指令进入文件所在目录，然后输入命令`FC 文件名1 文件名2`。
	
	下图是一个使用FC指令，查看新旧两个game.js文件差异的例子：
	
	![](http://ww1.sinaimg.cn/large/6ab8b972gy1fg9jpik45gj20il0k0dgb.jpg)
	
	如果使用的是Mac，可以在terminal中使用diff指令来实现相同的功能。diff表示差别，是difference的缩写。使用方法：利用cd进入文件所在目录，然后输入命令`diff -u 文件名1 文件名2`，其中-u表示unified diff format（标准区别格式），这个参数可以使输出内容更易阅读。
	
	下图是使用diff语句，查看之前新旧两个game.js文件差异的例子，仅供参考：
	![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhofdlbirdj21ey0xk0zi.jpg)
	
	相比之下，还是diff的处理方式要直观得多。
	
	如果一个版本控制工具能够同时满足恢复先前版本的核心诉求，同时又能够提供各不同版本之间的对照功能，那可想而知对我们的日常工作会有多么大的帮助。
	
	Git就是这么一个出色的版本控制工具，而且它拥有上述以外更多丰富的功能。下面我们一一来介绍。
	
3. Git的初始化配置

	在正式介绍Git的使用以及指令之前，我们先来看看Git的配置。
	
	俗话说，工欲善其事，必先利其器。如果说好的工具，能够让用户拥有事半功倍的效率，那么好的配置，则更是让好工具如虎添翼。
	
	以下所做的配置，主要是为了实现以下几个功能：
	
	- 文件被修改但是尚未commit的情况下，在末尾的id处有\*提示
	
	- 按tab可以自动补齐未完成的git指令

	- 使用sublime作为执行commit，处理merge conflict等行为的编辑器。

	- 配置个人的用户名称和电子邮件地址，适宜的Git push策略以及merge conflict显示策略
	
	我们首先先来说一下，在 Windows操作系统中，应当如何设置你的工作空间，来实现上述的功能。Mac下的操作也基本类似。
	
	1. 先上网搜索Git，选择你的操作系统对应的版本进行下载安装。

	2. Git bash的背景颜色修改：Git bash窗口的上方，右键，选中options，在弹出窗口的左侧选择Looks，右侧colors单词下方点击background修改背景颜色，foreground更改指令文字颜色。这一步可以根据个人的喜好。
	![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgbvrm5sggj20os09dwff.jpg)

	3. [在此处](https://www.udacity.com/api/nodes/3341718587/supplemental_media/bash-profile-course/download?_ga=1.37232743.672083044.1467344711)下载文件.bash\_profile\_course,将其移动到你的主目录中，然后重命名为.bash\_profile；将[此文件](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh)保存在你的主目录中，文件重命名为 git-prompt.sh，用于启用prompt中的git功能；
将[此文件](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash)保存在你的主目录中，文件重命名为git-completion.bash，用于启用tab自动填充功能。

		打开文件.bash\_profile进行查看，可以大概了解配置的具体状况。
		
		![](http://ww1.sinaimg.cn/large/6ab8b972gy1fge9f8t6pqj20i60eut9f.jpg)

		文本中的第2行意为加载git-completion.bash，启用tab自动填充功能；第5-8行定义了一些颜色，用于第16行Git提示信息的颜色设置。16行prompt的提示信息设置，会将用户名显示为紫色，检出的commit及其他Git相关的内容显示为绿色，当前所在目录后面跟个美元符号显示为蓝色，再之后的所有内容显示为默认颜色（reset）。但是由于我认为Git bash默认的提示信息颜色设置还不错，所以我在第16行前加入\#将该行配置予以屏蔽；第11行意为加载git-prompt.sh文件，这对于在你的提示符（prompt）中显示与git相关的内容是非常必要的；第12行表示如果你在Git代码库中更改了任意文件的内容，提示信息将会显示一个星号；第18行，为sublime程序路径设置一个subl的别名，方便今后在Git中启动sublime。添加内容为alias subl="C:/Program\ Files/Sublime\ Text\ 3/sublime_text.exe"。
		
		关闭文件.bash\_profile并再次打开Git bash，以上配置才会生效。
		
	4. 下载Sublime，配置Git使用sublime作为执行commit，处理merge conflict等行为的编辑器。方法：在Git bash中运行命令git config --global core.editor "'C:/Program Files/Sublime Text 3/sublime_text.exe' -n -w"，其中-n表示sublime将在新窗口中打开，-w表示Git将等待你关闭Sublime然后再继续后续的操作，‘’中是sublime程序所在的路径，请视各自安装情况填写。

		之后在Git Bash中敲入Sublime的完整路径，即可启动Sublime。如下图所示：
		
		![](http://ww1.sinaimg.cn/large/6ab8b972gy1fge9n8fd7jj20gi095aa6.jpg)
	
		![](http://ww1.sinaimg.cn/large/6ab8b972gy1fge9860ywkj20yr0exgmk.jpg)

		由于前面在git-completion.bash中的第18行，对Sublime的完整路径做过别名处理，因此之后如果想在Git中用Sublime打开某个文件，只需要在Git bash中运行指令subl+文件名即可。
		
		譬如，如果想用Sublime查看文件.bash_profile，运行指令：subl .bash\_profile即可。如下图：
		
		![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgea4sjb9ej20yf0euq45.jpg)
		
		在Mac系统中，这一步的实现方法也是基本相近的：

		![](https://ws4.sinaimg.cn/large/006tKfTcgy1fggkgiejmsj31kw0nf1ky.jpg)

		但是值得注意的是，Mac中应用程序的所在路径并不直观。要想了解Mac中应用程序的内部文件结构，可以在Applications下的应用程序上，按右键，在弹出菜单上左键点击Show Package Contents,继续点击进入后续文件夹，你最终会发现该应用所在的最终位置。

		以下是Sublime应用程序文件位置的查找方法：

		![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhpnrndd1qj216q0omwrd.jpg)

		![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhpns2afxfj21lm0o8aiu.jpg)

		确认其应用的最终位置是：Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl。之后，同样在.bash\_profile文件中为sublime程序路径设置一个subl的别名，方便后续的快捷打开。


	5. 配置个人的用户名称和电子邮件地址，适宜的Git push策略以及merge conflict显示策略

		第一个要配置的是你个人的用户名称和电子邮件地址。这两条配置很重要，每次 Git 提交时都会引用这两条信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录。具体的设置命令如下：
		
		git config --global user.name "你的用户名"
		
		git config --global user.email "你的email地址"
		
		更详细的内容，请参考[起步 - 初次运行 Git 前的配置](https://git-scm.com/book/zh/v1/起步-初次运行-Git-前的配置)一文。
			
		大部分情况我们想要做的只是Push当前的分支, 那么最适合的就是upstream。我们可以通过git config去配置采用upstream策略。具体的设置命令如下：
	
		git config --global push.default upstream

		关于Git Push策略的更详细内容，可以点击[此处](http://thekaiway.com/2013/07/30/config-your-git-push-strategy/)浏览。

		我们在使用Git合并分枝的时候，常常需要手工处理分枝冲突的情况。这时候我们可以用下面的设置来改进冲突标记使其显示冲突分枝之间共同的祖先（即，产生冲突之前的版本中共同的状态）。这个设置命令新添加一部分标记||||||| ，加入了共同祖先的注释。了解冲突行在冲突前的共同祖先处是什么状态，会比较有利于决策如何手工合并冲突。具体的设置命令如下：

		git config --global merge.conflictstyle diff3

		更详细的内容，请参考[解决 Git 冲突的 14 个建议和工具](http://blog.jobbole.com/97911/)一文。

	配置完成后，我们关闭并再次打开Git bash，大致检查一下配置是否生效。
	
	1. 首先来看看如果更改了文件内容，保存好但是没有及时commit，Git bash的ID处是否会出现星号。
	
	   我们来试试看，先输入指令vim game.js；
	   
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg6rwby8nj20gf08z74d.jpg)
	   
      回车后，在Git bash中打开game.js文件；
      
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg6v861qxj20gf096dga.jpg)
	   
	   输入o，在当前行之后插入一行（这里是在第一行后插入一行）
	   
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg6yo8w3yj20gh093aac.jpg)
	   
	   按esc键，结束插入
	   
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg71mnjxzj20gh0910t0.jpg)
	   
	   输入:wq，按回车，保存文档修改并退出。
	   
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg761xajwj20gh093dg9.jpg)
	   
	   退出文档后发现，之前的id后出现了星号，表示这个修改尚未被commit。
	   
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg78yc2abj20gj095dg5.jpg)
	   
	   重新输入vim game.js，打开文档，输入dd，按回车后，当前行被删除。再输入:wq，再按回车，保存文档修改并退出。文档恢复到了之前的状态，同时我们也发现，之前id后的星号也随之消失了。说明该功能配置成功。
	   
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg7f4pf5mj20gh094t93.jpg)
	   
	   更多Vim命令合集，请参看[参考资料：Vim命令合集](http://www.cnblogs.com/softwaretesting/archive/2011/07/12/2104435.html)。

	2. 我们再来看一看tab自动补全功能。
	
		在Git bash中先输入git -l
		
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg8odpfd7j20gg0900sy.jpg)
	   
	   接着，敲入1次tab键，没有反应。再敲入1次tab键，Git会将可能匹配的指令推荐给我。从下图中看到，这里Git推荐了git lfs和git log这两条可能匹配到的指令。
	   
	   ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgg8rajgoyj20gi0933yo.jpg)
	   
	   如果开始输入的是git lo，再输入tab，这时由于尽可能匹配到git log这一条指令，这时系统就会自动补齐指令为git log了。说明该功能也已配置成功。

4. Git的常用指令介绍

	Git的初始化配置完成后，我们可以来看一看一些常见的Git指令，一边使用，一边体会Git的强大功能。
	
	- git clone
	
	  当我们需要拷贝一个已经存在的Git repository副本的时候，我们会使用git clone指令。该指令的格式是：
	  
	  `git clone [url]`
	  
	  该指令的作用是，在当前路径下，创建相应的文件夹，并且初始化.git目录，然后从该url中拉取该repository的所有数据，并且checkout到当前最新commit的版本下。
	  
	  所以说不要将该指令理解成为下载最新commit的文件，事实上它的作用是是下载所有历史版本的数据记录。
	  
	  使用git clone之前，请先进入你想要下载文件的目录，之后使用git clone指令，会直接把代码库下载到该目录下。
	  
	  譬如，我要将一个asteroids工程的repository下载到桌面上。那么我就必须先进入desktop，再使用git clone指令下载整个repository。下载完毕后，再进入相应工程的目录中，这时候就可以在路径信息后看到该repository的分枝信息了。接下来就可以对该工程文件进行相应的git操作了。详细步骤请参看下图：
	  
	  ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgapnqz6nfj20go0begna.jpg)

	- git log

	  当我们想要了解该repository下详细的版本存档信息（commit），这时就可以使用git log指令对其进行详细的浏览。
	  
	  git log中包括了每次commit时记录的消息和相应的id号。

	  ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgaq5h3xb8j20h609saae.jpg)
	  
	  需要注意的是，如果使用windows下的Git bash，输入git log之后，如果log记录很多，超出屏幕的大小，此时是无法通过下拉屏幕右侧的滚动条来查看超出部分的log记录的，这时应该使用下箭头来查看。按住下箭头不放，就可以继续浏览更早以前的log记录，一直到出现END字样，就是记录已经到头，全部结束了。
	  
	  ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgaqgrtj5wj20gg0kfjsa.jpg)
	  
	  Mac下，如果想要退出git log查看页面，返回之前的terminal页面，可以按按键q来实现。如果是windows平台下，则git log内容和之前Git bash仍然处在同一页面，但该页面上git log内容的保留数量则取决于你查看log时用下箭头下拉涉及到的数量。

	  如果想查看每次commit更改文件的统计数据，可以使用指令：`git log --stat`。
	  
	  ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhvd3by17pj215e1e0qc8.jpg)

	- git checkout

	  git checkout的适用范围其实相当广泛，既可以针对分枝又可以针对commit的检出。指令格式是：`git checkout commit ID/branch name`。其中commit ID可以用git log指令查看到，在不引起歧义的情况下，一般仅输入commit ID的前4位即可，否则需要输入更多的ID位数。
	  
	  借由git checkout指令，我们可以将repository下的所有文件重置到任一commit时的版本状态,就好像打游戏时load存档文件一样。这么一来，只要有良好的存档习惯（commit），就再也不用担心出现诸如项目在某个中间过程被改废了的情况，你可以放心大胆地在原有存档的基础上实践自己的想法。如果你使用过SVN则要注意，这和SVN的checkout不大一样。
	  
	  以下是用git checkout重置到某一commit版本状态的例子：
	  
	  ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgbuaqao36j20gh09374t.jpg)

	  这里我们注意到一个警告："You are in 'detached head' state…"。这里的head其实是指Git当前正工作于其上的commit，你把它理解成一个指针即可。出现该警告是因为要checkout到之前老旧的commit版本状态，所以你将它的头拆开（detach）了。Git认为这种情况值得警告的原因是，如果我们checkout了这个更早的commit并且做出了更改，那这时如果再次commit的话该commit会处在log的哪个位置呢？情况多少会变得有些复杂，所以git提供一些说明指导你如何处理这种情况。

	  现在，当我检出这个更早的commit时，如果再次输入git log会发生很有趣的现象。这时，我们发现25ed变成了最新的commit，而之前更新的3条commit则完全没有显示在git log中。
	  
	  ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fgbue0aftrj20nd0kh3zm.jpg)

	  虽然没有显示在此刻的git log中，但之前更新的3条commit并没有被删除。我们依然可以通过之前最新的commit ID返回到最新的commit版本。
	  
	  ![](http://ww1.sinaimg.cn/large/6ab8b972ly1fgbum4rn23j20j60j9gml.jpg)

	  那么如果你把先前最新的ID给忘了呢？也没有关系，我们可以使用指令：`git checkout --detach master`来恢复初始head所在的版本位置。
	
    ![](http://ww1.sinaimg.cn/large/6ab8b972gy1fhvfplrjxij212q0qkq98.jpg)
    
      关于git checkout的更多详细内容，请参看[git checkout 命令详解](http://www.cnblogs.com/hutaoer/archive/2013/05/07/git_checkout.html)。
	  
	  
	
	

	
	
