---
published: true
author: Robin Wen
layout: post
title: "备份与恢复的一点思考"
category: 数据库
summary: "数据安全对于普通人而言会很陌生，然而早已在 DBA 心里生根发芽。数据对于一家企业的重要程度不言而喻，个人数据的管理也是极其重要，否则当数据损坏或者永久丢失，那将是毁灭性的灾难。根据墨菲定律，凡是可能出错的事必定会出错。在计算机世界里，没有任何系统、任何组件是 100% 靠谱的。在架构世界里，高可用是非常重要的考虑点。在现实世界里，也有很多黑天鹅事件。做好数据安全策略，比如软件开启云同步、数据备份多份、Time Machine 云备份、Dropbox Plus 云备份、定期淘汰硬盘、重要文件加密、有条件做 NAS等。数据是无价的，不要等到数据无法恢复时再后悔莫及。"
tags:
- 数据库
- Database
- 安全
- Security
---

`文/robin`

数据安全对于普通人而言会很陌生，然而早已在 DBA 心里生根发芽。数据对于一家企业的重要程度不言而喻，个人数据的管理也是极其重要，否则当数据损坏或者永久丢失，那将是毁灭性的灾难。

![Dropbox plus](https://cdn.dbarobin.com/mQWnful.jpg)

既然提到备份与恢复，笔者简单介绍下 MySQL 数据库的备份与恢复。按照备份后产生的副本文件是否可以编辑，可以将 MySQL 的备份方法分为逻辑备份和物理备份。逻辑备份可以简单理解成跟版本无关的 SQL 文件，物理备份是磁盘文件的快照。数据备份期间，按照是否需要停止 MySQL 服务实例，可以将 MySQL 的数据恢复分为：冷备份、温备份和热备份。线上系统中，温备与热备使用较多，冷备常常用于归档。按照副本文件的缺失程度可以将数据备份分为完全备份以及增量备份。比如我们使用 mysqldump 备份，指定了 --all-databases 参数，此时就是一个完全备份。另外，我们可以使用 Percona 公司提供的 xtrabackup 工具实现完全备份与增量备份。线上系统，我们需要针对不同的业务场景采用合理的备份策略，定期巡检，并且做好备份恢复测试。另外，我们还可以根据备份需求，设计一套备份平台。

好了，MySQL 数据库的备份与恢复就讲到这里。

时光回到 2017 年 9 月，macOS High Sierra 公测版可以对外下载。macOS High Sierra 最大的变化是文件系统升级为 APFS，按捺不住激动心情的我，花了一个晚上下载，然后在线升级。结果悲剧的事情发生，升级完成之后不能进入系统，进入恢复模式重装也不行。万幸的是，升级前手工备份了重要文件，基本保证了数据的可用。不过还是有少量文件丢失，损失尚可接受。折腾许久，最后只好采用在线重装，版本回退到 macOS Sierra。

经历这样一次数据灾难，开始反思自己的备份策略。从 9 月到现在两个月的思考和践行，个人认为还是很有参考价值，在此和读者分享。

**第一，所有软件开启云同步。**

一个软件对于用户而言，包含了数据和配置，如果软件提供了云同步功能，我们可以保证软件数据的安全。这里有一个建议，如果软件集成了 Dropbox，我们最好选择 Dropbox 进行数据备份。那配置文件呢？接下来我们展开讲讲。

**第二，mackup 备份配置文件。**

前面我们提到了数据的备份，这里讲一下配置文件怎么备份。配置文件备份推荐使用 [mackup](https://github.com/lra/mackup)，这是一个使用 Python 编写的开源的配置文件备份工具。我们可以利用 mackup 将配置文件备份到 Dropbox，软件配置稍有变更，立即同步到 Dropbox。除了同步到 Dropbox，mackup 还支持同步到 Google Drive、Copy、iCloud、Box 等。目前 mackup 支持的软件众多，基本上常用的软件都有囊括。mackup 实际上是将本地的配置软件做了一个软链到 Dropbox 目录，比如个人 home 目录有一个 `gitconfig` 文件，mackup 就会做如下的软链：

> lrwxr-xr-x   1 robinwen  staff    41B Oct  2 08:53 .gitconfig -> /Users/robinwen/Dropbox/Mackup/.gitconfig

使用 mackup 备份配置文件非常方便，执行 `mackup backup` 即可备份，如果要恢复，执行 `mackup restore` 即可。读者不妨尝试下。

**第三，数据备份多份。**

定期备份重要文件到移动硬盘也是很有必要的。很多时候我们并不会将重要文件同步到云，一来是这些文件比较隐私，二来这些文件可能比较大。我们可以制定一个策略，比如一周一次，定期将重要文件拷贝到移动硬盘的备份归档目录。正所谓不要把鸡蛋放在同一个篮子里，文件还需要存储几个副本。比如一个重要文件损坏、误删或者丢失，我们希望达到的效果是：可以从 A 移动硬盘恢复，也可以从 B 移动硬盘恢复，还可以从 Time Machine 备份恢复、还可以从 Dropbox Plus 云备份恢复。接下来我们接着讲 Time Machine 备份和 Dropbox Plus 备份。

**第四，Time Machine 备份。**

Time Machine 可以说是 Mac 平台目前最好的备份方案。Time Machine 真得像是时光机，可以自由穿梭到任何一个可以去到的地方。我们可以准备一个移动硬盘，选择非工作时间，将硬盘插入硬盘，打开 Time Machine，开启自动备份，让 Mac 在晚上继续飞吧。至于 Time Machine 专用移动硬盘需要多大，这个因人而异，取决于你的钱包和备份频率。一般用于 Time Machine 的专用移动硬盘至少是 Mac 硬盘总空间的 2 倍以上。Time Machine 第一次备份是全量备份，会占用比较大的磁盘空间，当然我们可以排除不必要的文件。第一次全量备份之后，以后的备份都是增量备份，占用空间会比较小。这里有一个建议，Time Machine 开启加密备份。读者想想啊，Time Machine 备份可是 Mac 的全量拷贝，如果没有加密，假如移动硬盘丢失，别人拿到之后就可以完整地恢复，细思恐极。为了最大程度保障数据的安全，我们需要开启加密备份。这里有个技巧，不要在 Time Machine 设置加密，而是利用磁盘工具将移动硬盘加密，每次备份之前输入磁盘的加密密码，这样备份过程才会比较顺畅。如果使用 Time Machine 提供的加密，它的机制是等备份完成再加密，你将会发现从晚上等到第二天白天，进度条还在那里，不增不减，很是恼人。另外，在 AppSo 还有一系列 Time Machine 使用教程 [^1]，读者可以参考下。

![Time Machine](https://cdn.dbarobin.com/x1uMLOK.png)

**第五，Dropbox Plus 云备份。**

数据是无价的，假如 Mac 系统崩溃，假如移动硬盘损坏，假如平时又没有做任何备份，那这样数据灾难带来的损失是无可估量的。我们需要为美好的事物付费，Dropbox 就是其中之一。因为一些不可描述的原因，Dropbox 无法正常访问，但这并不能阻碍 Dropbox 成为一款成功而优雅的云同步工具。准备地说，Dropbox 是同步盘而不是云盘。Dropbox Plus 和 Dropbox Pro 都只有 1T 的空间。1T 的空间对于正常的用户已经足够了，一个人一生的重要文件并没有这么多。当然如果你把一些影音文件放 Dropbox，笔者也帮不了你。每年 99 美金的价格，对于视时间为生命的人来说，一点也不昂贵。自从用上了 Dropbox Plus，所有重要文件实时同步，这丝滑顺畅的用户体验简直太赞。如果你想本地存一份，本地修改然后实时同步到 Dropbox，没有问题，我们可以借鉴 mackup 的实现，实际上就是利用软链。比如有一个 Work 的目录，只需要执行 **ln -s ~/Documents/Work ~/Dropbox/Documents** 就可以同步到 Dropbox。相信我，Dropbox 绝对值得拥有，当然，推荐之后对我并没有丝毫好处。

![Dropbox Plus](https://cdn.dbarobin.com/t8IATrp.png)

至于为什么不选国内的网盘，简单讲就是不信任，天知道国内厂商会拿这些文件做啥，还有某网盘无故删除用户文件之类的已经是家常便饭。除了 Dropbox，笔者认为还可以考虑 Google Drive。至于为什么不推荐 iCloud，从 Apple 将在贵州建立数据中心来看[^2]，不再信任 iCloud 了。当然这是笔者的判断，至于怎么取舍还是读者自行分析。其实即使 Apple 不在贵州建数据中心，iCloud 这用户体验依然很糟糕。

**第六，定期淘汰移动硬盘。**

刚好 2017 年 10 月又发生一件事情，大学时间就在使用的移动硬盘莫名其妙地就不能识别了。好在之前有做数据迁移，里面基本上没有什么重要文件。这里有一个常识，硬盘是有寿命的，我们需要整理一个移动硬盘表格，里面包含移动硬盘的生产时间、购买时间、使用时间、存放文件类型列表、硬盘重要程度等。通常移动硬盘使用 3 年左右就需要更换了，我们需要提前准备好新的移动硬盘，将旧的移动硬盘上的文件转移过去。

**第七，重要文件加密。**

备份与加密是对孪生兄弟，没有加密的备份还是不靠谱的。我们可以使用 Python 编写自动生成随机密码的脚本，然后对重要文件压缩加密。随机密码的实现方式，我们可以自定义一个数据字典，比如包含大写字母、小写字母、数字、特殊符号，然后随机生成密码。密码的位数最好 32 位以上，笔者通常都是使用 64 位的密码对重要文件进行加密。

讲完个人在备份上的思考和践行，接下来我们再来看下霍炬老师的备份方案：

> 1. 备份主机是一台安装了 FreeBSD 系统的 NAS ，用 ZFS 把硬盘组成 raid-Z 做为存储系统。
> 2. 在各计算机和 NAS 上安装 [syncthing](https://syncthing.net)，设置需要备份的文件目录和 NAS 同步，这样就把全家各台机器，包括虚拟机内部需要备份的文件都放到了 NAS 的存储上。syncthing 本身支持比较简单的文件版本，但是我没使用这一特性，主要使用它的同步功能。文件版本通过 ZFS 的 snapshot 功能实现。
> 3. 开源版本的 ZFS 没有原生加密功能，而对于备份系统，加密是必须的。所以我在 FreeBSD 上使用 PEFS 做为加密方案，缺点是加密之后会使得 ZFS 压缩功能几乎失效，不过无所谓，硬盘空间并不值钱，何况前面说过，规划好需要备份的重要文件本身也不会太大。
> 4. 使用 ZFS 快照并且做远程同步，我所知道的最好工具是 [zrep](http://www.bolthole.com/solaris/zrep/)。在我的系统上，使用 zrep，每 10 分钟对已加密文件系统做一次快照，并把快照同步到异地节点。同步节点同样需要使用 FreeBSD 和 ZFS。
> 5. 我设置了两个快照同步节点，一个较快的节点位于附近城市，一个较慢的节点位于另外一片大陆。 我实际使用案例中，这两个节点分别位于蒙特利尔和北京。 加上我自己家里的 NAS，三个节点可以保证在人为灾难（硬件损坏，火灾）和自然灾害（地震，水灾）等影响下仍然至少存活一个备份，是比较可靠的方案。
> 6. 最后需要提醒的是，用作备份的 ZFS 系统，只应该使用 BSD/Solaris，其他系统上 ZFS 的移植可靠性没那么高。[^3]

看完霍炬老师的备份方案，实在是汗颜，真极客。后续笔者也打算自建 NAS，对数据进行容灾备份。

根据墨菲定律，凡是可能出错的事必定会出错。在计算机世界里，没有任何系统、任何组件是 100% 靠谱的。在架构世界里，高可用是非常重要的考虑点。在现实世界里，也有很多黑天鹅事件。做好数据安全策略，比如软件开启云同步、数据备份多份、Time Machine 云备份、Dropbox Plus 云备份、定期淘汰硬盘、重要文件加密、有条件做 NAS等。**数据是无价的，不要等到数据无法恢复时再后悔莫及。**

最后，笔者开通了圈子，期待你的加入。

> 本圈子名字来源于同名博客「[https://dbarobin.com](https://dbarobin.com)」。
> 圈子建立初心：与价值观趋同的人交朋友。
> 本圈子有但不仅限于：「数据库知识和经验」「软件应用分享」「科技人文」「文章评论」「音乐艺术」「哲学哲思」等一系列看上去乱糟糟的独创或者二次信息传播。
> 我们生存在三个世界中，第一个是真实的世界，第二个是互联网世界，第三个价值世界。希望我们能在价值世界里自由行走。

![知识星球](https://cdn.dbarobin.com/9dhXNpn.jpg)

[^1]: [Time Machine 使用教程（一）：设置 Time Machine 备份你的 Mac](https://sspai.com/post/30550)
[^2]: [为什么在贵州？苹果中国首家数据中心有这些考量](http://tech.sina.com.cn/it/2017-07-13/doc-ifyiamif2743406.shtml)
[^3]: [做一个病毒卷土重来时代的幸存者](https://mp.weixin.qq.com/s?__biz=MjM5MTE4Nzk1NA==&mid=2650741750&idx=1&sn=4b9ce4c4a5b019a29c8592e6186f2da7)

–EOF–

版权声明：自由转载-非商用-非衍生-保持署名<a href="http://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh" target="_blank">（创意共享4.0许可证）</a>
