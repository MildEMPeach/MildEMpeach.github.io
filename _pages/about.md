---
permalink: /
title: "my home page"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---


## 自我介绍
各位老师好，非常荣幸有机会来到贵校参与夏令营活动。我是ygh，来自吉林大学计算机学院网络空间安全专业。前五学期专业绩点排名8/115。在校期间目前为止，获得过一次校一等奖学金，一次校优秀学生。语言方面，四六级均已通过，雅思今年上半年考过一次7.5。关于项目方面，利用互联网资源做过Gitlet项目，一个用java语言写的类似于git的版本控制系统；此外，也参与过学校老师的一个横向项目，负责做开源软件对国产操作系统的适配。科研方面，我的经历比较欠缺，这是因为在大一大二的时候忙着转专业考试和转专业之后的补修课程。上次有幸来到东大是三年前综合评价的时候，但很遗憾高考分数不够，今天很荣幸能再次来到这里。以上就是我的自我介绍。谢谢。

## 英语

### 有关数学建模
1. First, we quantify the data so spearman method can be implemented. With which we analyse the relationship between the wearthering and the color, type and pattern of the ancient glass. Then, we divide the data into two groups: the glasses that are weathering and are not. We calculate average, medium, maximal, minimal of different chemical compositions. Taking a deep comparison between whether weathering, we can predict the composition of the glass before they get weathering.

2. We select a few special and important chemical compositions, on which we implement K-Means method to classfy the data into two types. And then in each of them, we use the same method for further classification.

3. Now we get the model of classification, and we can make use of the data of different composition to predict the type of the unknown glass.

4. With grey-correnlence-analysis, we pick up some criticial compositions as mother sequence, and the left as child sequence. Calculate and draw the graph, we can see the relationship directly by the graph.

### 有关对于网络安全的理解

It would not be too much of a stretch to say that much of today’s world is built upon the Internet. Many of the services that run on top of the Internet come with their own class of vulnerabilities and defenses to match.

web security, which covers a class of attacks that target web pages and web services, such as sql injection, cookies and session management ans so on.

Three basic principles: confidentiality, intergrity and availability.  


## 项目

### 有关数学建模
1. 利用斯皮尔曼相关系数的分析方法，量化了数据，并分析了玻璃的颜色、类型、花纹与其是否风化的关系。将数据分为风化和未风化的两类，对于不同的化学成分求取平均值、中位数、方差、最大值和最小值。并根据比较得出的规律预测了风化前的成分。
2. 选取比较特殊的化学成分，利用K-MEANS聚类分析模型对数据进行分类。对于两种不同的种类，再利用同样的方法进行亚类划分。
3. 根据之前聚类得到的分类模型，通过关键成分的数据，进行分类。
4. 利用灰色关联分析法，挑选某些关键成分作为母序列，其余成分作为子序列，计算并作图，直观体现其关联性。

### 有关Gitlet
文件结构：
1. HEAD文件：保存了当前的分支名
2. heads文件夹：保存了所有的分支文件，名称为分支名，每个文件的内容为对应分支的最新commit的SHA1code。
3. commits文件夹：保存了所有提交的commit，文件名为commit的sha1code。
4. blobs文件夹：保存了所有跟踪的文件，文件名也是内容的sha1code。
5. stage文件：两个Map,用来存放下一次commit需要做改变的文件。

关于命令：
1. init：
初始化一个gitlet仓库，初始化以上文件夹/文件，进行第一次initial commit。

2. add:
添加文件，首先与当前最新的commit进行比较，如果当前commit中不包含该文件或者该文件的内容有改变，那么将该文件加入stage；否则需要清空stage中关于该文件的状态（如果有的话）。

3. remove:
删除文件，首先与当前最新的commit进行比较，如果commit中不包含该文件，要么该文件在stage中，删除在addstage中该文件，要么就是一个无效操作；如果commit中包含该文件，那么将该文件加入removestage中，并且删除当前文件夹中的该文件。

4. commit:
创建一个新的commit，其中commit中的map先复制一份当前commit的map，随后将该map与两个stage进行比较：如果两个map均为空，那就nothing to commit；否则依次按照两个stage添加、修改、删除文件名-shacode的映射关系。最后把两个stage清空。更新当前heads/当前分支的内容为最新的commit的shacode。

5. log/global log
log是按照时间顺序从最新开始依次输出每一个commit，读取当前最新的commit，按照链表的方式往前读取parent，如果有多个parent，读取第一条。

6. find
找到指定message的commit。获取commits下所有的commit，将其文件名放入一个List中，遍历这个List，根据文件名遍历读取每个commit，并比较commit的message和指定的message是否相等。

7. status
首先遍历heads文件夹，读取所有的分支名，当前分支前面加一个星号；然后依次读取addstage和removestage的key即可。

8. checkout
用法一： 获取最新commit中的某个文件的版本，并将其放入当前文件夹内。获取最新的commit，然后获取该文件的blob的shacode，根据code寻找blobs的文件，并将其内容写入该文件中。

用法二： 获取某个commit的某个文件的版本，比用法一多一个指定commitId的参数。

用法三： 切换到某个分支，首先根据切换的分支名在heads中找到对应分支文件，文件的内容即为该分支所在的最新的commitId，根据该commitId在commits文件夹中找到该对应的commit，也就是即将要切换到的状态；获取现在所在的最新commit进行比较。如果某个文件在futurecommit中出现，但是最新commit中没有且出现在了当前文件夹中，那么视为untracked，不作任何操作并提示信息。如果没有出现untracked的文件，那么就进行commit的切换。对于某个文件，如果当前commit中不存在该文件而futurecommit中存在，那么直接将该文件放入工作目录；如果两者都存在并且内容不等，覆盖该文件；如果futurecommit中不存在，当前存在，那么删除该文件。stage清零，并且更新当前所在分支名。

9. branch
创建一个新的分支，要求名字不能与已经存在的分支名相同，在heads文件夹中，创建一个以分支名为文件名的新文件，将当前的commitId作为其文件内容。注意，创建分支并不进行分支的切换。

10. rmbranch
删除一个已经存在且并不是目前所在的分支，根据分支名找对应文件，删除文件即可。

11. reset
将当前分支的commit回滚到某个指定的commitId上。

12. merge
执行merge前，stage必须清空；得到当前commit和将要合并的分支所在的commit，如果两者相等，那么不能与自己合并；否则找到最近公共结点（BFS）。

根据祖先结点，两条分支的结点，根据不同情况，进行merge。

两种特殊情况：祖先结点 = 当前commit，那么直接checkout 另一分支；祖先结点 = 另一分支commit，那么merge结果即为当前commit，不作任何操作。

其他情况： 产生一个merge后的commit，将文件分为不同类别，作相应操作：

文件存在于三个commit or 两个分支的commit：
    一个文件在一条分支被修改，而在另一条分支上并未修改，则该文件为被修改后的文件；

    一个文件在两条分支都被修改了，如果修改的内容相等，那么文件为被修改后的文件；如果修改的内容不等，则出现conflict，将两个文件的内容合并成一个文件，并指明出现了conflict的情况。

文件存在于某一个分支的commit：
    一个文件在某个分支之后出现，且只在这个分支出现，保留这个文件；（new）

文件存在于两个commit且这两者commit中该文件并未修改且其中一个为祖先commit：
    一个文件在某一个分支被删除，删除该文件。

### 有关国产方德操作系统

主要负责基于maven构建的java项目。具体的工作流程就是在github或者gitee上面找到相关的开源软件，git clone下来，根据maven相关编译指令尝试编译。将编译的指令过程，写在spec文件里面。打包软件包和spec文件，将这些东西传送到项目方提供的一个编译构建平台叫zebra上面，zebra会根据spec文件，执行指令，在虚拟环境中测试x86,arm,loongarch,sw64四种架构的cpu。测试通过之后，会自动将软件打包成rpm包。我再对这个rpm包做测试，比如写一个简单的java程序，证明rpm安装之后，这个软件或者架构是可用的。

## 专业课

或许只能随缘了。
