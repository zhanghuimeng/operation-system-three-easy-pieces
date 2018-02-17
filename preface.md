# 前言

## 致所有人
欢迎来看这本书！我们希望你享受阅读本书的过程，就像我们享受撰写本书的过程那样。这本书的书名是**《操作系统：三堂简单的课》**（Operating Systems: Three Easy Pieces）[^1]，显然，这是对有史以来最棒的课程讲义，《费曼物理学讲义》（Six Easy Pieces: Essentials Of Physics Explained By Its Most Brilliant Teacher）的致敬。{{ "F96" | cite }} 毫无疑问，本书达不到这位著名物理学家设置的高标准，但它仍可能在你理解何为操作系统（或者更广义地，系统）的征程上祝你一臂之力。

“三堂课”指的是组成这本书的三个专题：**虚拟化**（virtualization），**并发**（concurrency）和**持久化**（persistence）。这些概念的介绍过程将涉及到操作系统中的大部分关键要素；希望你们能在学习过程中得到乐趣。学习新东西是很有趣的，对吧？至少应该是这样。

每个主要概念将由一系列章节来进行介绍，大部分章节会指出一个具体问题，然后介绍如何解决该问题。每一章都很短，并尝试（尽最大的努力）给出想法来源的参考资料。本书的写作目的之一是理清操作系统发展的历史脉络，因为我们相信这能够帮助学生更清晰地理解操作系统的过去、现在和未来发展。举个例子：了解如何制作香肠和理解香肠的用途一样重要。[^2]

下面介绍一下本书中使用的很多思考和叙述方法。首先是问题的**症结**（crux）。任何时候，当我们在尝试解决一个难题的时候，都会首先尝试找出其中的核心问题，也即**问题的症结**；我们会在文字中明确强调问题的**症结**是什么，并在接下来的部分通过技术、算法和思想来尝试解决它。

我们会在很多地方通过展示系统随时间变化的行为来解释系统是如何工作的。这些**时间线**对理解起到了至关重要的作用；比如说，如果你明白，当一个进程页记录（process page）出错时会发生什么，你就几乎理解虚拟内存是如何运行的了。如果你能理解日志档案系统（journaling file system）将一块数据写入磁盘时会发生什么，就是向完全掌握存储系统原理上迈出了一大步。

书中还有很多**旁白**和**提示**，它们为主线介绍增添了很多色彩。旁白通常会讨论一些与主要内容相关（但很可能不是必要的）；提示通常是可以应用在你建造的系统上的通用知识。为了方便起见，书后列出了全部旁白、提示和症结。

我们在书中使用了**对话**这一最古老的教学方法，用以把一些材料用不同的方式展现出来。对话通常被用来介绍主要的专题概念（我们将会见到，那是一种极好的方法），以及偶尔的复习。它们也提供了用更幽默的方式进行写作的机会。你会不会觉得它们很有用或很幽默就是另一回事了。

在每个主要部分之前，我们都会展示操作系统提供的**抽象**，并在接下来的几章中介绍提供这一抽象所需的方法、策略以及其他支持。抽象对于计算机科学的各个方面都非常重要，所以它们在操作系统里也占据重要位置并不奇怪。

在每章中，我们尽可能地尝试使用**实际代码**（而非**伪代码**），因此，理论上来说，你可以自己运行所有例子。在实际系统上运行实际代码是学习操作系统的最好方式，所以我们鼓励你尽可能地这么做。

在课本的很多部分，我们加入了少量**作业**以确保你确实理解了所学内容。很多作业是对操作系统的部分的模拟；你们应该下载这些作业，然后运行它们。作业模拟器拥有以下特点：只要输入的随机种子不同，可以生成理论上无限种问题；还可以命令模拟器帮助你解题。因此，你可以不停地测试自己，直到你的理解达到了一定深度。

本书最重要的附录是一系列**项目**，你可以通过设计、编写和测试自己的项目代码学习真正的系统是如何工作的。所有项目（包括上面提到的实际代码例子）都是用C语言撰写的{{ "KR88" | cite }}。C语言是一种简单而强大的语言，大部分操作系统都是用C编写的，值得一学。有两种项目可供选择：第一种是**系统编程**项目，这些项目适合不熟悉C和UNIX，并且需要学习如何进行底层C编程的人；第二种项目基于MIT开发的操作系统内容xv6{{ "CK_08" | cite }}，这些项目适合已经熟悉C语言，想亲身感受一下实际的操作系统的人。在威斯康辛大学，我们用三种不同的方式来教授这门课程：全部是系统编程，全部是xv6编程，或者是两者的混合。

## 致教育者

如果你是希望使用这本书的讲师或教授，请随意。你很可能已经注意到了，[http://www.ostep.org](http://www.ostep.org)上提供了本书的免费在线版本。你也可以在[lulu.com](lulu.com)上购买纸质版本，购买方法请参见网页。

对本书的正确引用如下：

> Operating Systems: Three Easy Pieces
> Remzi H. Arpaci-Dusseau and Andrea C. Arpaci-Dusseau
> Arpaci-Dusseau Books
> March, 2015 (Version 0.90)
> http://www.ostep.org

使用本书作为教材时，如果课程时间为15周，那么应该能够以合理的难度水平涉及大部分主体。但如果把时间压缩到10周，那么就需要舍弃一些细节。我们通常会压缩关于虚拟机监控程序（virtual machine monitors）的几章，把它们安排在虚拟化专题的最后部分，或者作为学期最后的附加内容。

本书中有些不寻常的是，在许多操作系统教材中被放在前面的主题，并发（concurrency），被推后到学生对CPU和内存已经有基本的了解的时候。在我们教授这门课将近15年的过程中，我们发现，如果学生还没有理解什么是地址空间（address space）和进程（process），以及为什么上下文切换（context switch）会方式在任意时刻，他们就很难理解为什么会发生并发问题。但是，一旦他们理解了这些概念，介绍线程（thread）和并发问题的产生就变得容易了，至少是更容易了。

我们尽可能用黑板（或白板）来授课。在过去更概念化的日子里，我们在头脑中准备几个主要想法和例子，然后来到教室，用黑板来展示它们。讲义可以给学生提供与课程内容相关的具体问题。在现在更实用化的日子里，我们直接把笔记本电脑插到投影仪里，然后展示实际代码；这一方式对于并发相关的课程和讨论课非常实用，因为你可以把与项目相关的代码展示给学生。我们通常不用幻灯片来展示材料，但现在已经为喜欢这种上课方式的人制作了一份幻灯片。

如果你需要这些材料，请给我们发送电子邮件。我们已经把这些材料分享给了世界上的很多人。

最后一个请求：如果你使用这些免费的在线章节，请不要直接拷贝它们，而是提供章节的对应**链接**。这会帮助我们跟踪使用情况（在过去几年中下载了超过一百万次！），并保证学生能够得到最新最棒的版本。

## 致学生

如果你是一位阅读本书的学生，谢谢！我们很荣幸能够在你学习操作系统的过程中助你一臂之力。我们本科生时的一些课本（比如，Hennessy和Patterson 的《计算机体系结构：量化研究方法》{{ "HP90" | cite }}，这是一本计算机体系结构方面的经典教材）给我们留下了非常好的印象，我们希望这本书也能成为你的美好回忆之一。

你可能注意到了，这本书是在线免费阅读的。[^3]这样做的最大原因是：总的来说，课本太贵了。我们希望这本书是未来的免费课程材料浪潮中的第一本，这将会帮助世界各地的各种收入水平的学生接受教育。就算未来没有更多的免费材料，至少这是一本免费的书，比没有要好。

我们尽可能地在书中指出材料的原始出处，那些塑造了现在的操作系统的伟大的论文的研究者。思想不是凭空蹦出来的，而是聪明而刻苦的人想出来的（包括很多图灵奖获得者[^4]），因此我们应该努力赞美这些思想和思考者。我们希望这可以帮助你们理解历史上曾经发生过的变化，而不是把这些思想当做是一直存在的。{{ "K62" | cite }}更重要的是，这些参考文献可能会鼓励你进行自己的探索；阅读这一领域的著名论文无疑是最好的学习方法之一。

## 致谢

这一节的内容是感谢那些帮助我们撰写这本书的人。现在请听好：**你的名字也可以出现在这里！**但你需要帮助我们。所以请给我们一些反馈，帮助我们找出这本书中的错误。这样你就能出名了！或者，至少你的名字会出现在这里。

帮助过我们的人包括：Abhirami Senthilkumaran*, Adam Drescher* (WUSTL), Adam Eggum, Aditya Venkataraman, Adriana Iamnitchi and class (USF), Ahmed Fikri*, Ajaykrishna Raghavan, Akiel Khan, Alex Wyler, Ali Razeen (Duke), AmirBehzad Eslami, Anand Mundada, Andrew Valencik (Saint Mary’s), Angela Demke Brown (Toronto), B. Brahmananda Reddy (Minnesota), Bala Subrahmanyam Kambala, Benita Bose, Biswajit Mazumder (Clemson), Bobby Jack, Bjorn Lindberg, Brennan Payne, Brian Gorman, Brian Kroth, Caleb Sumner (Southern Adventist), Cara Lauritzen, Charlotte Kissinger, Chien-Chung Shen (Delaware)*, Christoph Jaeger, Cody Hanson, Dan Soendergaard (U. Aarhus), David Hanle (Grinnell), David Hartman, Deepika Muthukumar, Dheeraj Shetty (North Carolina State), Dorian Arnold (New Mexico), Dustin Metzler, Dustin Passofaro, Eduardo Stelmaszczyk, Emad Sadeghi, Emily Jacobson, Emmett Witchel (Texas), Erik Turk, Ernst Biersack (France), Finn Kuusisto*, Glen Granzow (College of Idaho), Guilherme Baptista, Hamid Reza Ghasemi, Hao Chen, Henry Abbey, Hrishikesh Amur, Huanchen Zhang*, Huseyin Sular, Hugo Diaz, Itai Hass (Toronto), Jake Gillberg, Jakob Olandt, James Perry (U. Michigan-Dearborn)*, Jan Reineke (Universitat des Saarlandes), Jay Lim, Jerod Weinman (Grinnell), Jiao Dong (Rutgers), Jingxin Li, Joe Jean (NYU), Joel Kuntz (Saint Mary’s), Joel Sommers (Colgate), John Brady (Grinnell), Jonathan Perry (MIT), Jun He, Karl Wallinger, Kartik Singhal, Kaushik Kannan, Kevin Liu*, Lei Tian (U. Nebraska-Lincoln), Leslie Schultz, Liang
Yin, Lihao Wang, Martha Ferris, Masashi Kishikawa (Sony), Matt Reichoff, Matty Williams, Meng Huang, Michael Walfish (NYU), Mike Griepentrog, Ming Chen (Stonybrook), Mohammed Alali (Delaware), Murugan Kandaswamy, Natasha Eilbert, Nathan Dipiazza, Nathan Sullivan, Neeraj Badlani (N.C. State), Nelson Gomez, Nghia Huynh (Texas), Nick Weinandt, Patricio Jara, Perry Kivolowitz, Radford Smith, Riccardo Mutschlechner, Ripudaman Singh, Robert Ordonez and class (Southern Adventist), Rohan Das (Toronto)*, Rohan Pasalkar (Minnesota), Ross Aiken, Ruslan Kiselev, Ryland Herrick, Samer Al-Kiswany, Sandeep Ummadi (Minnesota), Satish Chebrolu (NetApp), Satyanarayana Shanmugam*, Seth Pollen, Sharad Punuganti, Shreevatsa R., Sivaraman Sivaraman*, Srinivasan Thirunarayanan*, Suriyhaprakhas Balaram Sankari, Sy Jin Cheah, Teri Zhao (EMC), Thomas Griebel, Tongxin Zheng, Tony Adkins, Torin Rudeen (Princeton), Tuo Wang, Varun Vats, William Royle (Grinnell), Xiang Peng, Xu Di, Yudong Sun, Yue Zhuo (Texas A&M), Yufui Ren, Zef RosnBrick, Zuyu Zhang。我们特别感谢那些带星号的名字，因为他们对如何改进此书给了非常好的建议。

……（TODO）

## 最后的话

叶芝有一句名言：“教育不是灌满一桶水，而是点燃一把火。”[^5]这句话半对半错。你确实需要稍微被“灌点水”，这些文字显然是用来帮助教育你的；毕竟，当你参加谷歌的面试，他们问了你一个如何使用旗语的刁钻问题时，最好还是得知道旗语是什么。

但叶芝的话显然也有对的一方面：教育真正的意义是使你对某件事更感兴趣，开始自学关于它的更多知识，而不仅仅是在课上得到好分数。我们之一的父亲（Remzi的父亲，Vedat Arpaci）曾经说：“学习应当是超出课堂的。”

我们撰写这本书的目的是激发你对操作系统的兴趣，希望你能够阅读更多这方面的材料，向你的教授了解这一领域正在进行的激动人心的研究，甚至参与到研究当中。操作系统是一个非常棒的领域（！），充满了激动人心的伟大想法，它们不断地重塑着计算机的历史。我们明白，不是所有人都会对这一领域感兴趣，但希望至少有一些，或者几个人会受到这本书的鼓舞。因为，一旦求知的火焰被点燃，你就真正能够开始做一些伟大的事。这就是教育真正的意义：前进，去学习许多崭新而令人着迷的主题，在学习中成长，最重要的是，找到能真正激励你，为你点燃心中的那团火的事物。

*Andrea和Remzi夫妇*
*威斯康星大学计算机科学系教授*
*希望我们能成为点燃火种的人*[^6]

## 参考文献

{% references %} {% endreferences %}

## 注释
[^1] （译者注）本书书名待定。
[^2] 提示：香肠是用来吃的！或者，如果你是一个素食主义者，那香肠就是用来在看到的时候赶紧跑掉的。
[^3] 一些离题的话：在这里，“免费”并不代表开源，也不表示这本书不受到通常的版权保护。“免费”的意思是，你可以把这些章节下载下来，用来学习操作系统。为什么这本书不像Linux那样是开源的呢？因为我们相信，在一本书中只有一种声音是很重要的，我们为了提供这种感觉努力了很久。当你阅读这本书的时候，你应该感觉像是有人在向你解释什么东西。这就是我们的方法。
[^4]图灵奖是计算机科学界的最高奖项；它相当于诺贝尔奖，区别是你从未听说过它。
[^5]如果这句话确实是他说的。就像许多名言一样，它的历史十分暧昧不明。
[^6]如果我们听起来像纵火犯，那么你的重点大概错了。如果这句话听起来过于做作和多愁善感，那是因为确实如此，不过请原谅我们吧。