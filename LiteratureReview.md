# 众包与移动众包文献综述

## 一.    众包
众包的概念是在2006年在美国 《连线》 杂志2006年的6月刊上，该杂志的记者Jeff Howe首次提出的。众包是直接将任务发布到互联网，通过开放式集合互联网上未知的大众来解决传统计算机单独难以处理的问题。目前已经有许多成功的众包网站案例，国外最早的众包网站AMT(Amazong Machinical Turk)， Crowd Flower，Cloud Crowd ，Wikipedia等，国内的网站有猪八戒，脑力库，三打哈，百度百科，百度知道等。
	目前的众包平台主要分为两种，协作式众包与竞争式众包，协作式众包主要是工人之间相互合作来完成一个任务，竞争式众包主要是工人都提交问题的答案，由提问者或者众包平台从中找出最优的答案，之前介绍的Wikipedia、百度百科都是协作式众包平台，AMT，猪八戒都是竞争式众包平台。
	众包平台的参与者主要是两个主体，提问者与众包工人。提问者向众包平台提出问题，众包平台将问题发布给众包工人，众包工人向众包平台提供问题答案，众包平台分析后将最终答案交给提问者。 
	在众包平台内部，主要分为四个模块，任务设计，工人质量分析，问题答案聚合，任务分配。
提问者将问题提交给众包平台，首先进入任务设计模块，将提问者的问题规划为统一的格式，之后进入任务分配模块，根据质量分析模块得到的质量将问题分配给众包工人，众包工人的答案提交到答案聚合模块，该模块将分析出最终答案并将答案提交给提问者【33】。
目前关于众包的科研工作主要分为五个个部分，众包平台及系统，质量控制，任务分配，答案聚合，其他众包问题，接下来我们将对这五个个方向的研究现状做逐一介绍。  

###  1.众包平台及系统  
众包任务的完成需要通过众包平台来实现，一个众包平台要想持续运营，其最严峻的挑战就是众包任务的质量，而如何保证高质量的众包结果的输出，每个平台都有其不同的方法。本文将给出一些众包平台和系统以及其解决众包问题的方法。
Argonuat【1】，由Daniel Haas及其团队提出的一个解决大文本量的数据处理任务的平台，例如从大量的数据存储形式不同的商业站点中提取餐馆的菜单的信息，如菜品的名称、价格和描述等。其采用分层评级的方法来提高Macrotask工作质量。首先通过使用工人质量预测模型选择出可信度高的工人。其次，Argonuat使用任务误差预测模型将出错率高的任务分配给受信任的工人，并随时间的推移追踪工人的质量。通过在企业中运行Argonuat系统大约3年左右的时间，执行了超过130万条任务，最终验证了Argonuat系统与random spotchecking方法相比，在误差捕获性能方面提高了118%。
Chimera【2】，由Chong Sun及其团队提出的一个对大规模数据进行分类的系统，即将数百万种产品分成5000以上的类别。该系统首先初始化一个人为创建的分类规则，利用这个规则筛选出需要由分类器进行处理的数据，该系统提供三种分类器，rule-, attribute-, and learning based，每种分类器都要对产品进行分类（得到的是分类的权重），通过voting和filter将分类结果进行组合以获得最终结果，对结果进行取样，经由众包工人对结果进行评价，判定为错误答案的结果将返回，并基于该评价由analysis修改规则，将规则反馈回系统，重新运行系统，直到取样的准确率足够高。Chimera方法已成功在walmart.com上应用，并实现了将2500000个产品的90%进行了分类，并达到了90%的准确度，在众包资源方面，评估1000个产品仅需15-25个工人工作一个小时。
Icrowd【3】，由清华大学李国良教授提出的一个多问题类型的众包系统，ICROWD将任务分成了很多类别（例如娱乐类，体育类，科学类等），根据任务的类别，每个工人在不同类别上会有不同的质量，根据工人对不同类别问题的质量来个性化的给工人分配任务，这种分配方式比传统的方式更加细化。这个系统的特点是，工人的质量不是一个值而是针对多个问题类别的向量，Icrowd首先建立一个贝叶斯网络，将各种问题以及其相关性放到一起，对于每个工人，建模对于不同类型问题的质量，每当有新的问题时，系统会首先对问题进行归类，然后再将问题分配给相关类型高质量的工人，不仅如此，本文的方法还可以根据不同类型问题之间的关联度来计算工人没有回答过问题的质量。
由此可见，工人是否可靠是决定众包质量的关键，而设计一个稳健的众包平台，工人的可靠性是首先要考虑的问题。
  

### 2.质量控制  
由众包工人收集上来的结果往往存在脏数据和有歧义的数据，因此需要有效的方法解决此问题以得到高质量的结果。现有的研究提出了多种质量控制技巧，这些工作的基本思路是使用某种工人模型来描述工人质量，例如计算工人概率（正确率或错误率），使用矩阵模型来描述工人回答问题的能力等【34】。
2.1工人概率
将工人的质量描述为一个介于0到1之间的工人概率p，用此概率来表示工人正确（或错误）地回答一个问题的概率。
香港科技大学Lei Chen和Caleb Chen Cao及其团队提出Jury Selection Problem(JSP) 【4】，主要解决选择几个工人（group）作答以及选择哪几个工人作答的问题。该论文提出计算Jury（k个工人）error rate的方法，即先计算出每个工人的error rate（先基于twitter datas对retweet action进行图构建，用户为图的节点，再基于图对用户进行排序，最后根据已给公式计算，该公式所使用的参数为排序的最大最小值），再利用概率计算k个工人的error rate，即jury的error rate（在这过程中遵循了majority voting），理论上选取error rate最小的jury，而在PayM模型中还应考虑每个工人的个人需求，使得工人组合（即jury）的整体需求小于等于给定budget。该文分别在合成数据和真实微博数据上进行了验证，证明本文分别基于两个模型提出的算法是十分高效及有效的，使用这两个模型的时间复杂度分别在O(n2) 和O(nlog n)时间内。
由于P的定义是一个概率，p的范围受限于0到1之间，Manas Joglekar和Hector Garcia-Molina的团队将工人概率p拓展，引入置信区间来计算工人的错误率的受信程度。
文献【5】对于每个工人𝑃𝑖（错误率）的值提供一个估计(Pi) ̂， 使得𝑃𝑖 有一个在置信水平𝑐𝑖的情况下，半区间大小为𝜖𝑖的置信区间，也就是说，有𝑐𝑖%的概率，工人真实错误率𝑃𝑖介于(Pi) ̂−𝜖𝑖 到(Pi) ̂+𝜖𝑖之间。具体的方法是，统计每组工人对答案相同的个数。然后通过Wilson Score Interval公式分别求出三个工人的错误率的estimate。进而使用f函数得到错误率estimate的置信区间，以此来表征工人的质量。多个工人的做法与三个工人类似，选择第一个工人，将剩余的工人分为两个不相交的集合，把这两个集合代表两个工人，以此来求得第一个工人的置信区间，进而求得全部工人错误率的置信区间。实验采用三个真实的数据集：IC(image comparison), SOT(Schools of Thought)和MOOC (Massive Open Online Course)，选择某一个置信水平，运行general differences scheme检查工人的真实错误率是否落在算出的置信区间当中。实验结果表明该算法可以去除表现差的工人并提供准确度较高的置信区间。
在此之后，Manas Joglekar和Hector Garcia-Molina的团队在上述工作的基础上做了进一步的改进，提出的算法适应于更加广泛的情形【6】：1）工人可以做任意数量的任务；2）任务的答案选项可以是k元的；3）能够发现工人做任务的偏好。首先使用ProbEstimate 算法求得工人答案概率矩阵的点估计，根据工人频率矩阵和概率矩阵的关系，先求出频率矩阵对应的特征值和特征向量，进而得到工人概率矩阵的单位阵，通过单位阵求出工人概率矩阵的点估计；再用调用Algorithm A3求得工人答案概率矩阵的置信区间。实验结果表明工人回答的任务的个数越多，跟理想的情况就越接近；工人每个任务都完成的概率越低，则错误率的置信区间就越大；同时，增加答案选项的个数置信区间的平均大小会增大。
2.2矩阵模型
矩阵模型用于描述工人回答问题的能力。该模型通常为
M=[■(M_1，1&⋯&M_(1，n)@⋮&⋱&⋮@M_(n，1)&⋯&M_(n，n) )]
M_(j，k)通常表示一个条件概率，即当任务的正确答案为j时，工人给出答案为k的概率。
Akash Das Sarma及其团队针对众包质量管理问题【8】。即给出一组工人的答案和对应的任务，目标是估测出任务真正的答案和工人的质量。以前基于EM算法的方法没有理论的保证。文中提出一个globally 最优算法OPT来估测任务正确答案以及工人质量，算法概念化的考虑了所有从任务到答案的映射，因为考虑全部可能的映射数量难以管理，所以利用了两个方法Bucketizing和Dominance Ordering来减少映射数量。实验使用真实数据和模拟数据对于OPT与EM算法进行比较，结果显示OPT算法效果更优。

2.3其他模型
众包问题通常是成组发送给工人，这种一组问题在amazon里被称为HIT，在众包工人回答问题时，同一个HIT中的不同问题会相互影响，从而导致工人给出了错误的答案，基于这样的背景，文章【7】结合Plackett-Luce model建立了一个工人模型，在通过一个改进的EM算法来获取问题的答案，通过这种方式消除了同一个HIT内不同问题的影响，从而使答案更加精确。
当前众包中对工人质量的应用主要有两个方向，一个是假设所有的工人拥有相同质量，这种方法简单但是获取的答案准确率很低，另一个是采用EM算法迭代的获取工人质量，这种方法获取的答案精度较高，但是EM算法本身复杂度过高所以这种方法的效率很低，Incremental【9】这篇文章结合这两种方法的优缺点提出了一种基于增量的工人质量推理方法，文章设计了一个工人模型和一个问题模型，工人模型是一个基于混淆矩阵改编的矩阵，问题模型是一个多元向量，采用贝叶斯原理来计算获取工人质量，实验证实这种方法既能获取相对较高的准确率，也能保证算法效率。
小结
质量控制要描述或者建模工人的质量，主要用工人的正确率（或错误率）来表示一个工人正确（或错误）回答一个问题的概率和矩阵模型用来描述工人回答问题的能力，此外还有针对于具体问题提出的相关的模型。
  

### 3.答案聚合
  通过众包的方式我们可以得到大量的工人答案，这时的首要问题就是如何从大量答案中聚合出问题的最终答案，也就是答案聚合。 
	当前的答案聚合主要有三个研究方向，majority voting（大多数投票），weight majority voting（基于权重的大多数投票），other problems（其他的问题）。
	Majority voting是一种相对简单的答案聚合方法，这种方法假设所有的工人质量相同，最终的答案只和回答的工人数量有关，当前很多众包平台CrowdDB,DECO采用的都是这种方法。这种方法获取答案的效率很高，但是由于工人的知识背景与答题经验的不同，实际上每个工人的答案的可靠性是不同的，因此这种方法的准确率很低。
	Weight majority voting是一种考虑了工人质量的voting方法，当前主流的方法都是基于这个方法实现的，【15】，【16】，都是采用的这种方法，【15】中提出了一种基于众包解决rating和filtering问题的算法，传统解决这种问题的方法存在的问题是假设工人质量相同，假设一定有先验信息。本文作者提出了一种ANSWER-RECORD模型和POSTERIOR-BASED模型。通过这两个模型来使文章中提到的算法普遍化。【16】提出了一种基于worker confidence来计算问题答案的方法，将工人回答问题的准确率转化成confidence，将worker confidence转化成answer confidence比较不同答案的confidence来得到最终的答案。
	在答案聚合领域，还存在许多其他的问题，【13】提出了在众包任务的答案聚集阶段因数据不足而导致最终得出的结果真实性不高的问题。使用了迁移学习transfer learning的方法，提出一个分层贝叶斯模型hierarchical Bayesian model, TLC (Transfer Learning for Crowdsourcing)，模型将重复的用户作为桥梁来借助辅助的历史信息评估出工人对于特定任务的能力值，以提高结果数据的真实性。通过用真实数据将TCL和MV,GLAD,DARE方法进行比较，结果显示TCL的效果更好。【14】提出了针对于众包数据聚集过程中工人在不同的topic下能力不同的问题[5]。为了获得工人在不同topic下的专业水平，本文提出一个FaitCrowd，（a fine grained truth discovery model），分别对问题的内容和任务的答案进行概率建模，其中对于问题内容建模使用了一些自然语言处理的方法，通过FaitCrowd模型同时估测出工人专业技能和问题的真值并分配topic label给问题。实验通过用两组真实数据对于FaitCrowd和MV,TruthFinder等方法的比较，结果显示FaitCrowd的方法效果更佳。
【17】该论文针对多分类任务（区别于只有两个选项Yes or No的任务，该任务有多个选项）的答案生成问题，The Pennsylvania State University的Aditya Kurve, David J. Miller和George Kesidis，提出基于EM算法的随机模型，该模型的参数为工人意图（工人是恶意的还是诚实的），任务难度，工人技能，通过使用该模型不断迭代参数值，最终可以得到以上参数值以及任务答案。




### 4.其他众包问题
4.1打标签问题
Guoliang Li的团队利用众包的方式解决为POI( points of interest)打标签的问题【18】。众包给POI打标签还有以下难点：首先，与普通的标签相比，POI标签有着更复杂的影响因素，有名的POI会得到更高质量的回答；其次，工人与POI的距离会影响工人的质量；最后，工人是动态进入答题的，很难立即识别工人的能力并明确地分配任务。文中提出一个框架包括推测模型inference model和在线任务分配器online task assigner。推测模型首先根据工人的固有质量将工人分成两类，低质量的工人准确率为0.5，高质量工人,结合他的距离感知质量和POI的影响加权得出工人准确率，推测模型使用Graphical Probability Model来推理答案，使用EM算法推算参数。
南洋理工的Shuji Hao和Chunyan Miao等教授提出了一种通过众包的方式来获取数据标签的方法【19】。通过众包获取数据标签主要的挑战是存在给出错误答案的工人和问题提出者有限的预算资金。针对这样的问题本文提出了一种learning with expert的框架，通过这个框架可以从工人中找出准确率较高的工人，还提出了eliability-based allocation的方法，通过这个方法根据工人的可靠性来分配任务从而降低预算。通过在台湾国立大学的模拟数据集上进行实验，分别从不同的噪声环境中和其他方法进行对比，结果显示本文的方法在高错误率工人数量增加时，得出结果的准确率没有明显的下降。
Daniel Haas的团队在解决data labeling延时问题上也引入了众包【20】。Data labeling在数据分析中扮演着重要的作用，但其缓慢的过程阻碍了现代数据分析中交互系统的发展，因为manual labeling的延时性很高。因此Haas的团队提出了实现低延时的加速众包加速的系统，称之为CLAMShell。CLAMShell将延时分为三类，即per-task latency, batch-wise latency和end-to-end overall latency，并且使用Straggler mitigation, Pool maintenance,Hybrid learning和众包相结合的方法来解决三类data labeling延迟问题。通过模拟和在Amazon的Mechanical Turk平台的在线实验，验证了CLAMShell在data labeling的准确率上实现了8倍加速。
4.2实体融合问题
斯坦福教授Hector及其团队提出利用众包解决实体融合（Entity Resolution）问题【21】。传统的实体融合过程分为两个部分Pairwise Analysis(获得的是records对的相似值)和Global Analysis(输出是最终结果，即属于同一实体的记录的集合)，而Hector团队将Pairwise Analysis中获得的结果抽取出来以二元问题的方式询问众包工人，其中其创新点在于提出probabilistic framework，用来1.估计问每个问题得到多少ER精度；2.选择有最高期望精度的问题作为用来问的问题（这里的每个问题对应于前面的records对）。目标是选择尽可能少的问题，并获得高准确度。本文将Crowd ER算法分别在合成数据和真实数据上进行了测试，证明该算法确实在有效减少问题数量的同时获得了高准确度。
香港科技大学Chen Jason Zhang和 Lei Chen及其团队针对模式匹配（Schema matching）的问题【22】，提出让众包工人识别数据的语义进行模式匹配，将整体模式匹配分解成识别单个属性的一致性，例如两个模式A和B，都表示教员信息，其中{<(Professor)Name,Prof.name>, <Position, Position>,<Gender,Sex>, <(Department) Name, Department>}是一个可能匹配，让工人将其全部写出是比较困难的，但是只将其中一对抽取出来作为二元问题询问工人就简单许多。论文中使用香农熵来表示模式匹配结果的不确定性，值越大，不确定性越高。并且本文提供了选择一个问题和同时选择多个问题的方法，都是使用香农熵差来衡量其对结果不确定性的降低，这些问题的数量受到问题预算的约束。其中选择多个问题中是一个动态的循环过程，即系统每次选出K个问题，只要有一个问题答案被返回，系统就会重新运行，继续选择K个问题，从而保证问题永远是最新的。本文中的两个方法均进行了模拟同时在Amazon Mechanical Turk (AMT)进行了测试，实验证明当k的数量增加时，刚开始不确定性减少很快，但是不确定性较少的趋势渐趋于平缓，总体的时间效率是不断提升的。这同Question Selection for Crowd Entity Resolution中思想类似，在实体融合中是用准确度衡量，选取的问题是能够降低整体准确度的，而在解决模式匹配问题中，是采用熵来衡量，选取的问题能够降低整体的熵，从而提高匹配准确度。
花费、质量、时间的平衡．由于众包平台并不能够保证结果质量，因此结果质量控制一直是科研人员研究的重点．由于工人和任务请求人二者之间有着不可调和的矛盾（工人目的是得到更多的报酬，任务请求人则是想通过最少的钱快速地完成最多的任务），因此如何平衡任务的花费、任务的结果质量、任务完成时间三者的关系是一个重大挑战．
（1）	数据研究表明任务完成时间与众多影响因素（如请求人提交的任务数量等等）有关系，结果表明预测一个任务的完成时间是非常困难的。
（2）	一个任务的结果质量和很多因素有关，例如任务的难度、工人的负责程度、工人和任务的相关性等等。为了确保任务结果质量，任务请求人通常会将任务分配给多个人。
（3）	由于任务的金钱花费一般与任务数目和任务标价相关，因此一般是可控的。但是当任务数量很多的时候，单纯依赖工人来完成所有的任务需要的花费是巨大的．在发布任务之前，针对任务要求进行预处理可以减少任务数目。
（4）	当只考虑花费、质量、时间3个方面中的某一个方面，是比较容易控制的，但是花费、质量、时间三者之间的关系是很难衡量的，因此目前很多科研人员研究如何在三者之间进行平衡，从而达到某种优化目的。
Jinyang Gao,等人提出一个在众包系统中对于花费敏感的决策方法【23】。众包利用人的智慧来解决机器难的问题。但是由于工人都是基于他们的知识、经验和个人感知来解决众包任务，所以需要一个方法来分析这个任务用众包解决是否比仅仅用机器解决更好。文章中提出来一个针对众包花费敏感的决策方法。这个方法在线评估众包任务的利益，当一个任务没有未来利益了，就停掉任务，不再收取答案。由于不知道任务的答案是否正确，因此，文中计算任务的利益P的期望值来估测任务的平均利益。通过算法找出利益期望值最大的问题状态序列（question run）。


## 二、移动众包
  移动互联网与物联网等技术的飞速发展,使得众包数据管理技术从基于在线众包平台的模式转变为一种新型的服务模式,称为“时空众包(spatiotemporal crowdsourcing)”(也称为空间众包或移动众包)。移动众包通常是指通过移动互联网设备实时地在移动众包平台上汇聚众包任务与众包参与者,并通过平台对众包任务进行分配调度与质量控制,从而使众包参与者在物理世界完成众包任务并满足任务约束条件的过程。
  移动众包的主要参与者包括众包任务的请求者与众包参与者,他们通过移动众包平台建立联系。时空众包平台负责对所请求任务和参与者信息进行综合处理.一般地,平台首先将任务和参与者信息进行预处理,然后将其交给任务分配引擎。随后,任务分配引擎基于任务特点和优化目标进行任务分配，并将相应信息反馈给请求者和参与者。根据不同的任务需求,平台既可将任务执行结果直接反馈给请求者,也可对执行结果进行整合汇聚，再反馈给请求者【35】。
  目前关于众包的科研工作主要分为以下几个方面：任务选择、任务分配、质量控制与隐私保护。但目前已阅读的文献主要集中在任务选择和任务分配以及平台隐私保护三个方面，以下做逐一介绍。

#### 1.任务选择
  任务选择指的是工人自行在众包平台上挑选任务，一般有两种方式：一是工人在平台上搜索自己感兴趣的任务，即pull-based的方式；二是平台为用户推荐一些可供选择的任务，即push-based的方式。
  对于pull-based方式，Dingxiong Deng等人【10】在2013年提出WST模型（The worker selected tasks mode），旨在让工人选择的任务的数量最大化。给定一个工人、一组有时间、地点约束的任务，生成一个任务计划表，使得被执行的任务数量最大化。
  相比pull-based方式，push-based方式能够让工人获得更具有针对性、更感兴趣的任务。Dingxiong Deng, Cyrus Shahabi等人【10】在2013年提出了Maximum Task Scheduling (MTS)问题，利用工人活动范围和任务的截止日期，为工人推荐一组可执行的任务的计划表，工人按照该计划表执行任务，能够使完成的任务数量最大。Cen Chen 等人【11】的方法是根据工人的日常路线进行任务推荐，通过将推荐问题看作随机整数线性规划问题，假设工人的日常路线已知，将问题分解为agent-specific routing 子问题。每个工人都能够选择最适合自己行动路线的任务集，使更多的任务被选择，避免超代理现象。Yu Li等人【12】也是参考工人的历史行动轨迹，为工人推荐一条包含任务数量尽可能多的路线，工人走完该路线能够到底目的地，并且能够获得最多的收益。相比之前的工作，本文克服了动态规划路径的问题，有新任务到达时，能够及时更新路线。

#### 2.任务分配
  在任务执行阶段，将已存在的任务分配给合适的工人，以达到预期效果。预期效果可以是收集的答案的质量高，也可以是被执行的任务数量最大，不同的场景下会有不同的目的。	
  香港科技大学Lei Chen和Caleb Chen Cao及其团队【24】提出Jury Selection Problem(JSP)，目的是选择合适的工人，基于微博服务解决决策问题。在移动众包领域，进行任务分配时需要考虑的因素更多。Leyla Kazemi , Cyrus Shahabi【25】【26】等人在2012年提出了MTA（Maximum Task Assignment）问题，即最大数量任务分配问题。工人向服务器发送一个请求，内容包括工人的工作区域和最大可接任务数量，服务器根据工人的这个请求给工人分配工作，不仅要满足该工人的条件，也要使得平台分配出的任务数量最大化。这种分配方式没有考虑任务的类型和工人质量，所以Cyrus Shahabi等人在2013年又提出了MSA（Maximum Score Assignment），在分配时会将任务分配给更擅长这种任务的工人，例如将拍摄照片的任务分配给摄影师，通过解决图的最大加权二分匹配问题，完成任务分配。Y.Tong等人【27】在解决任务分配问题时，考虑到了工人和任务到达的随机性。在这样的动态环境中，根据众包平台的历史记录，将一天分为若干时间段进行分配。工人-任务对的权重等于工人完成任务的概率与该任务的报酬的乘积，对于随机到达的工人和任务，既要使得被分配的任务数量最多，也要使使得工人-任务对得总权重最大。所以本文对于每个时间段的前半段和后半段采取不同的分配算法，前半段时间寻找权重最大的对，后半段保证分配的数量。
	此外，如果任务的工作量大或者比较复杂的情况下，需要将这种任务分配给大于等于一个工人。针对这种情况，Cyrus Shahabi等人【28】 在2013年提出Maximum Correct Task  Assignment，为了收到预期的答案，会将任务分配给一组工人（>=1），这组工人的整体置信度达到指定的值。Hung Dang等人【29】定义了复杂任务分配问题MCTA（Maximum Complex Task Assignment），复杂任务由多个子任务组成，子任务之间有所联系。在进行复杂任务分配时，需要将所有的子任务都分配给工人，并且工人都完成被分配的子任务，才算是完成一个复杂任务。每个工人可以接受不同复杂任务中的子任务，每个复杂任务的子任务也可以分配给多个工人。
  
#### 3. 移动众包平台及平台中的隐私保护
 移动众包的任务完成是通过移动众包平台去实现，一般情况下，request通过平台发布任务，包括任务所在的位置，任务的报酬，任务至少需要多少个工人去完成以及任务的到期时间，worker则通过平台去查找并选择任务，或者平台根据特定的算法直接将任务分配给合适的工人。
Cyrus Shahabi等人【30】在2013年提出了一个移动众包的框架GeoCrowd，它由两个主要部分组成：一个是web服务器和一个是移动客户端。服务器可以接受request发布的空间众包请求（利用地图界面），这些请求被系统翻译成一系列的空间任务。在移动客户端，工人通过手机客户端，查找自己感兴趣的任务并去执行。这篇文章是一个demo，没有讲具体的实现，只说明了移动众包需要扩大规模，能够应用到对社会有重大影响的社会领域，比如救灾时的灾后重建。
由于在平台上发布任务，工人选择任务或者接受平台分配给他的任务的前提是你要在平台上进行注册，这就涉及到工人隐私的问题，Hien To 1, Gabriel Ghinita 2, Cyrus Shahabi等人针对隐私保护的问题【31】，提出了PrivGeoCrowd，一个在服务器进行任务分配的时候可以保护工人位置隐私并进行交互的可视化工具箱。平台与用户签订一份合同，规定了位置信息泄漏的条款和条件。
Zhao Chen，Rui Fu等人在2014年介绍了一个通用空间众包平台：gMission【32】。gMission主要有User Interface，Location Sensing，Task Recommendation，Quality Control四个模块。该系统的创新点在于它提供多种location sensing功能用于任务分配，如WiFi ﬁngerprint localization for indoor environment 以及 GPS-based localization for outdoor environment。与此同时，该系统采用了一种特殊的任务分配模型，该分配模型包括三个机制，Location Based Recommendation（选择停留时间短，距离任务点近的工人），Whom-to-ask Enhancement（考虑了每个工人的error rate以及k个工人的error rate），Load Balance Enhancement（考虑了工人当时的任务量）。

## REFERENCE
[1] D.Haas, J.Ansel, L.Gu and A.Marcus. Argonaut: Macrotask Crowdsourcing for Complex Data Processing. VLDB, 2015, 2015：1642-1653.
[2]C. Sun, N. Rampalli , F. Yang and A. Doan. Chimera: Large-Scale Classiﬁcation using Machine Learning, Rules, and Crowdsourcing. VLDB, 2014. 
[3]J Fan，G Li，BC Ooi，KL Tan，J Feng. iCrowd: An Adaptive Crowdsourcing Framework,Sigmod,2015:1015-1030.  
[4] C. Cao, J. She, Y. Tong and L. Chen. Whom to Ask? Jury Selection for Decision Making Tasks on Micro-blog Services. VLDB，2012:1495-1506 
[5] M Joglekar，H Garcia-Molina，A Parameswaran. Evaluating the crowd with confidence. KDD, 2014:686-694.  
[6] M Joglekar，H Garcia-Molina，A Parameswaran. Comprehensive and Reliable Crowd Assessment Algorithms. ICDE, 2014.  
[7] H Zhuang，A Parameswaran，D Roth，J Han. Debiasing Crowdsourced Batches, ACM, 2015:1593.  
[8] A.D.Sarma, A.Parameswaran, J.Widom. Towards Globally Optimal Crowdsourcing Quality Management: The Uniform Worker Setting. SIGMOD’16, 2016::47-62.  
[9] J Feng，G Li，H Wang，J Feng. Incremental Quality Inference in Crowdsourcing, DASFAA 2014: Database Systems for Advanced Applications pp 453-467.  
[10] Dingxiong Deng, Cyrus Shahabi, Ugur Demiryurek, Maximizing the Number of Worker’s Self-Selected Tasks in Spatial Crowdsourcing, SIGSPATIAL, 2013.
[11] Cen Chen, Shih-Fen Cheng, Hoong Chuin Lau, Archan Misra, Towards City-scale Mobile Crowdsourcing: Task Recommendations under Trajectory Uncertainties, ICJAI 2015.
[12] Yu Li, Man Lung Yiu, Wenjian Xu. Oriented Online Route Recommendation for Spatial Crowdsourcing Task Workers. SSTD, 2015.
[13] K.Mo, E.Zhong and Q.Yang. Cross-Task Crowdsourcing. KDD’13, August 11–14, 2013:677-685.  
[14] F.Ma, Y.Li, Q.Li, M.Qiu, J.Gao, S.Zhi,L.Su, B.Zhao, H.Ji, and J.Han. FaitCrowd: Fine Grained Truth Discovery for Crowdsourced Data Aggregation. KDD’15, August 10-13, 2015.  
[15]A.Parameswaran, S.Boyd, H.Garcia-Molina, A.Gupta, N.Polyzotis and J.Widom. Optimal Crowd-Powered Rating and Filtering Algorithms. Proceedings of the Vldb Endowment 2014, 2014：685-696. 
[16] X Liu，M Lu，BC Ooi，Y Shen，S Wu. CDAS: A Crowdsourcing Data Analytics System, VLDB,2012：1040-1051.  
[17] D Miller，A Kurve，G Kesidis.Multicategory Crowdsourcing Accounting for Variable Task Difficulty, Worker Skill, and Worker Intention, IEEE, 2014：794-809.  
[18]H.Hu, Y.Zheng, Z.Bao, G.Li, J.Feng and R.Cheng.  Crowdsourced POI Labelling: Location-Aware Result Inference and Task Assignment. In ICDE.2016, 2016
[19]S. Hao, S.C.H .Hoi, C. Miao and P. hao. Active Crowdsourcing for Annotation. IEEE Computer Society2015, 2015
[20]D.Haas, J.Wang, E.Wu and M.J.Franklin. CLAMShell: Speeding up Crowds for Low-latency Data Labeling. VLDB, 2015, 2015.
[21]S. Euijong Whang，P. Lofgren and H. Garcia-Molina. Question Selection for Crowd Entity Resolution. VLDB, 2013.
[22]CJ Zhang，L Chen，HV Jagadish，CC Cao, Reducing Uncertainty of Schema Matching via Crowdsourcing, VLDB,2013, 6(9):757-768.
[23]Jinyang Gao, Xuan LiuAn .Online Cost Sensitive Decision-Making Method in Crowdsourcing Systems. SIGMOD’13, June 22–27, 2013, New York, New York, USA.
[24] C. Cao, J. She, Y. Tong and L. Chen. Whom to Ask? Jury Selection for Decision Making Tasks on Micro-blog Services. VLDB，2012.
[25] Leyla Kazemi , Cyrus Shahabi. GeoCrowd: Enabling Query Answering with Spatial Crowdsourcing. ACM SIGSPATIAL, 2012
[26] Hien To, Cyrus Shahabi, Leyla Kazemi, A Server-Assigned Spatial Crowdsourcing Framework
[27] Y.Tong, J.She, B.Ding, L.Wang, L.Chen. Online Mobile Micro-Task Allocation in Spatial. ICDE, 2016, 2016
[28] Leyla Kazemi, Cyrus Shahabi, Lei Chen, GeoTruCrowd: Trustworthy Query Answering with Spatial Crowdsourcing, SIGSPATIAL, 2013.
[29] Hung Dang, Tuan Nguyen，Hien To, Maximum Complex Task Assignment: Towards Tasks Correlation in Spatial Crowdsourcing, iiWAS, 2013.
[30] Cyrus Shahabi, Towards a Generic Framework for Trustworthy Spatial Crowdsourcing, MobiDE, 2013:1-4. 
[31] Hien To , Gabriel Ghinita , Cyrus Shahabi, PrivGeoCrowd: A Toolbox for Studying Private Spatial Crowdsourcing, ICDE, 2015:1404-1407.
[32] Zhao Chen, Rui Fu, Ziyuan Zhao, Zheng Liu, Leihao Xia, Lei Chen, Peng Cheng, Caleb Chen Cao, Yongxin Tong, Chen Jason Zhang, gMission: A General Spatial Crowdsourcing Platform, VLDB, 2014:1629-1632.
[33] FENG J H, LI G L, FENG J H. Asurvey on crowdsourcing [J]. Chinese Journal of Computer, 2015, 38(9) :1713-1725. (in Chinese)
[34]G Li，J Wang，Y Zheng，M Franklin.Crowdsourced Data Management: A Survey,IEEE,2016,28:1-1.
[35]Tong, Y.X., Yuan, Y., Cheng, Y.R., et al. A survey of spatiotemporal crowdsourced data management techniques. J. Softw., 28(1):35-58 (in Chinese)
