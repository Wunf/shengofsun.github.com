---
layout: post
title: "Linus vs. Tanenbaum译稿(2)"
category: computer related
tagline: Linux过时了
tags: [os, debated]
---
{% include JB/setup %}

发信人: rburns@finess.Corp.Sun.COM (Randy Burns)<br/>
主题: 回复：Linux过时了<br/>
日期: 30 Jan 92 20:33:07 GMT<br/>
组织机构: Sun Microsystems, Mt. View, Ca.

　　在文章<12615@star.cs.vu.nl>中ast@cs.vu.nl (Andy Tanenbaum)说到:

>　　当然5年之后情况又会不同，但是5年之后大家早已纷纷在自己200MIPS、64兆的SPARC-5工作站上跑起免费的GNU系统了。

　　如果这事在将来能发生，让我含笑九泉我都行。

>　　写一个新的操作系统还紧紧依附于某个特定的硬件，尤其是像英特尔这样的怪胎，这根本就是错到家了。——这就是我的观点。

　　首先，Linux里面最和80x86紧密相关的部分也就是内核底层和设备驱动。我自己觉得吧，即便linux只是我们在用GNU内核之前的一个权宜之计，为一个现今使用量最多的系统结构专程设计一款内核也是很值得的。

　　OS就应该能够轻易移植到新的硬件平台上。

　　Linux里面唯一不可移植的部分就是内核底层和驱动。和编译器啦、工具包啦、窗口管理系统啦什么的比起来，这也只占很少的一点工作量。既然Linux在系统调用上和可移植操作系统有很高的兼容性，那我也没什么好吐槽的了。能有一个OS让我们更有可能利用来自Berkeley、FSF、CMU等处的软件，我个人对此双手点赞。两三年后，相当实惠的BSD变种和Hurd的使用量或许会激增，那时Linux才算真过时了。至于现在么，Linux大大降低了如gcc, bison, bash之类工具的使用成本，这对开发相当有好处——比如说开发OS。

------------
Linus Benedict Torvalds<br/>
发信人: torvalds@klaava.Helsinki.FI (Linus Benedict Torvalds)<br/>
新闻组: comp.os.minix<br/>
主题:回复:Linux过时了<br/>
日期: 31 Jan 92 10:33:23 GMT<br/>
组织机构: University of Helsinki

　　在文章<12615@star.cs.vu.nl> 中ast@cs.vu.nl (Andy Tanenbaum)说到:

>　　minix的局限性至少和我作为一个教授是有点关系的：minix一个极为明确的设计目标是它能够运行在便宜的硬件上，这样学生才能负担的起。

　　很好：十足的技术观点，也让我的一些评论毫无辩解的余地。但是同时你有点搬起石头砸了自己的脚：现在你终于承认了minix里面的一些问题纯粹是出于它太可移植了，甚至还囊括了那些压根不是为unix系统设计的硬件平台。这个假定引出了如下事实：尽管硬件支持，要在minix上添加一些像分页之类的扩展是没这么容易的。不错，minix是有很好的可移植性，但是你要是换个说法如”没有使用任何硬件特性”仍旧不错。

>　　一个多线程的文件系统只不过是一个性能上的技巧而已。

　　不敢苟同。在微内核架构上这是一个性能上的技巧，但当你写一个宏内核系统的话，你就能发现这是一个非常自然而然的特性，甚至都是一个微内核无法圆满完成的领域(我在给Andy Tanenbaum的个人邮件中已指出这一点)。当以”过时”的方式写一个UNIX的话，你很自然的就写出一个多线程的内核：每个进程各司其职，并且你也用不着为了提高性能去写诸如消息队列之类的丑陋代码。

　　另外，也总有人认为”仅仅一个性能上的技巧”是至关重要的：如我所料非错的话，除非你有一台cray-3，不然大家肯定都对长时间等待电脑响应头疼不已。我知道我在minix上就是如此(嗯，我在linux上也会这样，但是情况好多了)。

>　　我仍旧表示在1991年设计一款宏内核的系统是大错特错。幸亏你不是我的学生。这样的设计在我这儿是拿不了优的。

　　好吧，就算没有你，我十有八九也考不出什么好成绩：我已经在这个学校和一个教操作系统设计的老师吵了一架了(完全是出于另一见不相干的事——甚至都和OS没什么关系)。

>　　写一个新的操作系统还紧紧依附于某个特定的硬件，尤其是像英特尔这样的怪胎，这根本就是错到家了。——这就是我的观点。

　　但我的观点是操作系统是不依附于任何处理器硬件的：UNIX在现今绝大多数处理器上都跑的很顺畅。当然，怎么实现必须得看硬件，但这和”依附”是大大不同的。你把OS/360和MS-DOS作为糟糕设计的典型，因为它们依赖于硬件，这点我同意。但它们和linux完全不是一回事，linux的API是可移植的(不是由于我的设计有多么巧妙，而是由于我决定效仿一个在设计、实现和实践中都经过千锤百炼的系统：unix)

　　你现在为linux写程序，等你在21世纪想移植到Hurd上了你重新编译一下就好了，对此你必然不会大吃一惊。前面也提到了(不光是我说的)，linux内核只不过是完整的系统里的九牛一毛：linux代码现在全加起来打个包也就大概200KB——开发一个像样点的完整系统打包好的代码量少说也得10个兆(并且很容易说多就多出一大堆)。除了这个微乎其微的内核之外，剩下的代码也都是可移植的。更何况就算你什么都不懂，从头写一个这样的内核也用不了一年(事实上我就是这样的)。

　　其实整个linux的内核加起来也远比Mach内核中和386相关的代码少的多：Mach当前版本的i386.tar.z打包文件超过了800KB(据nic.funet.fi数据，是823391个字节).诚然，mach作为一个”像样的”系统还要大些并且还有更多的特性——你们完全可以从中去琢磨出点什么东西　(译者注：考虑到Mach是微内核的，所以译者认为Linus仍然在嘲讽微内核)。

Linus

------
发信人: kaufman@eecs.nwu.edu (Michael L. Kaufman)<br/>
主题: Re: LINUX is obsolete<br/>
日期: 3 Feb 92 22:27:48 GMT<br/>
组织机构: EECS Department, Northwestern University

　　我试着在工作的时候发这两封邮件的。但是它们好像没发出去。如果你们已经看到了下面的信件，请原谅。

---------

　　Andy Tanenbaum写了一篇很搞笑的文章(发现他也上这个新闻组同样也很搞笑)，但是我觉得他忽略了很重要的一点。

　　他说道:

>　　很多人都知道，对我来说MINIX是一个业余爱好。

　　对于绝大部分玩Linux的人，我相信这也是事实。我们并未开发一个要占领OS市场的系统，我们只是乐在其中。

>　　它们不会在哪一天突然消失，而是会逐渐取代80x86的地位。它们会通过模拟80386的软件来运行那些老旧的MSDOS程序。

　　如果这件事真的发生了，而我还是想玩Linux的话，我完全可以在我386的模拟器上面跑它们。

>　　MINIX在移植性上的设计较为合理。并且已经从英特尔的处理器移植到了68000,SPARC,和NS32061的芯片上。LINUX和80x86绑的太紧密了。这不是正道。

　　对于有那些机器的人来说这是好事，但这其实是把双刃剑。可移植性的代价就是386性能和特性的损耗。在你决定说Linux不是正道的时候，你应该自己考虑一下你要用它来做什么。我要用它在我的486计算机上跑对内存和计算量都有很高要求的图形程序。对我来说，速度和内存要比什么所谓未来艺术上的优雅和可移植性重要多了。

>　　但凭心而论，对于那些想要一个够现代够免费的OS的人们，我真心建议他们找一个基于微内核的可移植的OS，比如像GNU或者其他类似的。

　　我从来没听说过什么基于微内核的可移植的操作系统。GNU现在仍旧只是水月镜花，并且在可以预见的未来似乎依然会是这副样子。你有什么可推荐的么，或者你就是在寻我开心？

---------

　　在文章12615@star.cs.vu.nl中ast@cs.vu.nl (Andy Tanenbaum) 说到:

>　　写一个新的操作系统还紧紧依附于某个特定的硬件，尤其是像英特尔这样的怪胎，这根本就是错到家了。——这就是我的观点。OS就应该能够轻易移植到新的硬件平台上。

　　我觉得看到这儿我就不能赞同你了。你就是在拿OS设计里的一个结果来看待这个东西。Minix好是因为它可移植还基于微内核之类云云；Linux不好是因为它基于宏内核还紧紧绑在Intel上之类云云。这种态度扔学术界还不算奇怪，但是你如何让整个世界都信服？Linux不是写来教书的，也不是一个毫无实质意义的课后练习。写它是用来让人类在这个时代跑GNU软件的。重要的不是五年之后Linux也许会销声匿迹，而是现在我能用它想跑什么软件就跑什么软件。你继续吹捧你的Minix吧，反正它要是不能跑我想跑的软件，(在我眼里)它就是一文不值。

>　　10年前的MS-DOS是专门为8088写的，这就有点不太明智，但IBM和微软好歹还是在吃尽苦头之后意识到了这点。

　　我还是老说法。微软折腾个dos出来不是用来做”OS前沿领域研究探索”的，而是为了美元。并且考虑到MS-DOS现在仍旧卖的大红大紫，很明显他们目的已经达到了，所以我也不赞同你说他们不明智。虽然说不管从哪个角度看，MS-DOS都算不上什么好货，但它满足了市场的需求。

Michael

---------
发信人: richard@aiai.ed.ac.uk (Richard Tobin)<br/>
主题: 回复：Linux过时了<br/>
日期: 4 Feb 92 14:46:49 GMT<br/>
组织机构: AIAI, University of Edinburgh, Scotland

　　在文章12615@star.cs.vu.nl中ast@cs.vu.nl (Andy Tanenbaum) 说道:

>　　一个多线程的文件系统只不过是一个性能上的技巧而已。考虑到一般情况下一台个人电脑只有一个任务运行，做一个这样的技巧实在是费力不讨好。

　　我发现在用Minix的时候，单线程的文件系统是我永远的痛。在我从软盘读文件(速度慢的让人抓狂)的时候，我总是想去干点什么别的事情。在等待大一点的C程序或lisp程序编译的时候，我连打人的冲动都有。

　　还有就是我总是喜欢编译一个文件时在文本编辑器里看另一个文件。

　　(如果文件系统只管文件操作而不和终端IO交互的话，这个问题的严重程度貌似有点减轻。)

　　当然，考虑到Minix没有虚拟终端并且根本也跑不了Emacs，上面的问题似乎不是什么大问题。但是对于很多人来说，这完全是劣势，而不是优势。根本不是由于什么在单用户的机器上跑多个进程没有意义；是因为大家早就都适应了垃圾电脑和垃圾的操作系统，这样解释差不多你的这句话就说得通了。

　　至于移植性么，Minix是靠着它没什么野心和理想才能获胜。如果你想要个有分页、有任务控制、有窗口系统的功能齐全的UNIX，是给Minix内核添加这些特性快呢？还是修改一些386的权限位，给Linux添加来的快呢？我觉得这么去黑Linux实在不公平，因为它的定位和　　Minix是如此的不同。如果你想要一个教学工具，那么毫无疑问Minix。但是如果你想在你的个人电脑上要一个无限接近Sun工作站的环境，这就要另当别论了。

Richard

--------------
发信人: ast@cs.vu.nl (Andy Tanenbaum)<br/>
主题: 回复：Linux过时了<br/>
日期: 5 Feb 92 14:48:48 GMT<br/>
组织机构: Fac. Wiskunde & Informatica, Vrije Universiteit, Amsterdam

　　在文章6121@skye.ed.ac.uk中richard@aiai.UUCP (Richard Tobin) 说道:

>　　如果你想要个有分页、有任务控制、有窗口系统的功能齐全的UNIX，是给Minix内核添加这些特性快呢？还是修改一些386的权限位，给Linux添加来的快呢？

　　你好像完全忘记了还有一个选择：买一个UNIX或者是一份拷贝。如果你就是想用用系统，而不是玩到内核内部去，你根本用不着源代码。Conerent才99美元，并且还有更多功能更完善的也更贵的UNIX变种。对一个真正的黑客来说，拿不到代码等于要了亲命。但是对于那些只想使用UNIX环境的人来说，选择多的是(虽然不是免费的)。

Andy Tanenbaum (ast@cs.vul.nl)

----------
发信人: ajt@doc.ic.ac.uk (Tony Travis)<br/>
主题: 回复：Linux过时了<br/>
日期: 6 Feb 92 02:17:13 GMT<br/>
组织机构: Department of Computing, Imperial College, University of London, UK.

　　ast@cs.vu.nl (Andy Tanenbaum) 说:

>　　你好像完全忘记了还有一个选择：买一个UNIX或者是一份拷贝。如果你就是想用用系统，而不是玩到内核内部去，你根本用不着源代码。Conerent才99美元，并且还有更多功能更完善的也更贵的UNIX变种。对一个真正的黑客来说，拿不到代码等于要了亲命。但是对于那些只想使用UNIX环境的人来说，选择多的是(虽然不是免费的)。

　　Andy，自从minix第一条消息发布到这个新闻组上起，我就随着minix的不停开发在用minix了，我现在用的是Bruce Evans打了补丁的1.5.10版。

　　我只想在我的机器上要一个UNIX并且我也对玩内核没什么兴趣，但是我真的想要一份源代码！

　　潜藏在UNIX的成功和流行背后一条很重要的准则就是”要建立在别人工作的基础上”的哲学。

　　这种哲学的前提是源代码是可以获取的，这样大家才能在开发新软件时审核它，修改它，重用它。

　　很多年以前，我对AT&T UNIX V7的源代码许可证非常满意；后来，你决定让Minix的源代码也是可以随软件发行的，这件事也让我颇感开心，因为这是对AT&T后续版权枷锁的一种解脱！！

　　我想你有时候会忘记你的这项”业余爱好”已经对”个人版”UNIX(即，大家能买得起的UNIX)的可用性产生了深远的影响。事实上，我现在386/SX上minix的这份拷贝要比我8086PC上跑的Minix1.2 的价格便宜的多。

　　是的，Minix不可能成为每个人的全部，但是正如在68000或者其他的基于线性地址空间架构的处理器一样，我在386上也看到Minix的进步：这对于我们这群人是好事，我们用minix，也对PC版基于分段体系结构的minix感到很不爽。

　　不管你说什么，我也不会去用Conherent的。

Tony

----------
发信人: richard@aiai.ed.ac.uk (Richard Tobin)<br/>
主题: 回复：Linux过时了<br/>
日期: 7 Feb 92 14:58:22 GMT<br/>
组织机构: AIAI, University of Edinburgh, Scotland

　　在文章12696@star.cs.vu.nl中ast@cs.vu.nl (Andy Tanenbaum) 说道:

>　　如果你就是想用用系统，而不是玩到内核内部去，你根本用不着源代码。

　　很不幸的是玩内核是我们要一个系统的唯一目的。要想说服我们，还得得BSD变种或者是GNU内核出来了——估计也就是最近几个月的事儿了吧(也有可能是最近几年)。

Richard

