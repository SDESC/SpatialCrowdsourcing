# 众包与移动众包文献综述
## 1.    众包

###  众包的工人质量分析  
■ A.D.Sarma, A.Parameswaran,J.Widom. Towards Globally Optimal Crowdsourcing Quality Management: The Uniform Worker Setting. SIGMOD’16, June 26-July 01, 2016.
Akash Das Sarma及其团队针对众包质量管理问题[6]。即给出一组工人的答案和对应的任务，目标是估测出任务真正的答案和工人的质量。以前基于EM算法的方法没有理论的保证。文中提出一个globally 最优算法OPT来估测任务正确答案以及工人质量，算法概念化的考虑了所有从任务到答案的映射，因为考虑全部可能的映射数量难以管理，所以利用了两个方法Bucketizing和Dominance Ordering来减少映射数量。实验使用真实数据和模拟数据对于OPT与EM算法进行比较，结果显示OPT算法效果更优。  

### 众包的任务分配  
■	C. Cao, J. She, Y. Tong and L. Chen. Whom to Ask? Jury Selection for Decision Making Tasks on Micro-blog Services. VLDB，2012.  
针对基于微博服务解决决策问题的问题，香港科技大学Lei Chen和Caleb Chen Cao及其团队提出Jury Selection Problem(JSP) [12]，主要解决选择几个工人（group）作答以及选择哪几个工人作答的问题。该论文的创新点首先在于提出AltrM （Altruism Jurors Model）and PayM （Pay-as-you-go Model）模型描述众包工人在众包应用中的行为，并分别基于这两个模型定义了Jury Selection Problem(JSP)；其次提出计算Jury（k个工人）error rate的方法，即先计算出每个工人的error rate（先基于twitter datas对retweet action进行图构建，用户为图的节点，再基于图对用户进行排序，最后根据已给公式计算，该公式所使用的参数为排序的最大最小值），再利用概率计算k个工人的error rate，即jury的error rate（在这过程中遵循了majority voting），理论上选取error rate最小的jury，而在PayM模型中还应考虑每个工人的个人需求，使得工人组合（即jury）的整体需求小于等于给定budget。该文分别在合成数据和真实微博数据上进行了验证，证明本文分别基于两个模型提出的算法是十分高效及有效的，使用这两个模型的时间复杂度分别在O(n2) 和O(nlog n)时间内。  

### 众包问题的答案分析
■	K.Mo, E.Zhong and Q.Yang. Cross-Task Crowdsourcing. KDD’13, August 11–14, 2013  
Qiang Yang及其团队针对在众包任务的答案聚集阶段因数据不足而导致最终得出的结果真实性不高的问题[4]。使用了迁移学习transfer learning的方法，提出一个分层贝叶斯模型hierarchical Bayesian model, TLC (Transfer Learning for Crowdsourcing)，模型将重复的用户作为桥梁来借助辅助的历史信息评估出工人对于特定任务的能力值，以提高结果数据的真实性。通过用真实数据将TCL和MV,GLAD,DARE方法进行比较，结果显示TCL的效果更好。

■	F.Ma, Y.Li, Q.Li, M.Qiu, J.Gao, S.Zhi,L.Su, B.Zhao, H.Ji, and J.Han. FaitCrowd: Fine Grained Truth Discovery for Crowdsourced Data Aggregation. KDD’15, August 10-13, 2015.  
Fenglong Ma及其团队针对于众包数据聚集过程中工人在不同的topic下能力不同的问题[5]。为了获得工人在不同topic下的专业水平，本文提出一个FaitCrowd，（a fine grained truth discovery model），分别对问题的内容和任务的答案进行概率建模，其中对于问题内容建模使用了一些自然语言处理的方法，通过FaitCrowd模型同时估测出工人专业技能和问题的真值并分配topic label给问题。实验通过用两组真实数据对于FaitCrowd和MV,TruthFinder等方法的比较，结果显示FaitCrowd的方法效果更佳。

■	A.Parameswaran, S.Boyd, H.Garcia-Molina, A.Gupta, N.Polyzotis and J.Widom. Optimal Crowd-Powered Rating and Filtering Algorithms. Proceedings of the Vldb Endowment 2014, 2014  
斯坦福大学的Aditya Parameswaran与Stephen Boyd等教授提出了一种基于众包解决rating和filtering问题的算法[7]。rating和filtering问题就是指选择类问题，rating是多元选择问题，filtering是二元选择问题。传统解决这种问题的方法存在的问题是假设工人质量相同，假设一定有先验信息。本文作者提出了一种ANSWER-RECORD模型和POSTERIOR-BASED模型。通过这两个模型来使文章中提到的算法普遍化，可以不在上述前提的情况下解决rating和filtering问题。通过在MOOCs（大量开源课程）数据上进行测试，结果显示答案的错误率比传统方法低30%。



### 众包平台、框架、原型系统
■	D.Haas, J.Ansel, L.Gu and A.Marcus. Argonaut: Macrotask Crowdsourcing for Complex Data Processing. VLDB, 2015, 2015.    
Daniel Haas及其团队提出了有关Macrotask的众包问题[1]。所谓Macrotask，是指需要耗费大量时间的大文本量的数据处理任务，例如从大量的数据存储形式不同的商业站点中提取餐馆的菜单的信息，如菜品的名称、价格和描述等。针对Macrotask问题，主要的挑战是评估众包工人输出的质量，因为Macrotask任务的真值往往不容易得到。因此Daniel Haas及其团队提出了Argonuat，即一个采用分层评级的方法来提高Macrotask工作质量的框架。Argonuat首先通过使用工人质量预测模型选择出可信度高的工人。其次，Argonuat使用任务误差预测模型将出错率高的任务分配给受信任的工人，并随时间的推移追踪工人的质量。通过在企业中运行Argonuat系统大约3年左右的时间，执行了超过130万条任务，验证了Argonuat系统与random spotchecking方法相比，在误差捕获性能方面提高了118%。

■	C. Sun, N. Rampalli , F. Yang and A. Doan. Chimera: Large-Scale Classiﬁcation using Machine Learning, Rules, and Crowdsourcing. VLDB, 2014.  

针对大规模分类问题，University of Wisconsin-Madiso的Chong Sun及其团队提出Chimera[11]方法，当使用Chimera方法对items进行分类时，首先初始化gatekeeper（训练集和由分析师创建的分类规则），利用gatekeeper筛选出那些需要由分类器进行处理的items，该系统提供三种分类器，rule-, attribute-, and learning based，每种分类器都要对items进行分类（得到的是分类的权重），通过voting和filter将分类结果进行组合以获得最终结果，取样，经由众包工人对结果进行评价，判定为错误答案的结果将返回，由analysis修改规则，并将规则反馈回系统，重新运行系统，直到取样的准确率足够高。Chimera方法已成功在walmart.com上应用，并实现了将2.5M物品的90%进行了分类，并达到了90%的准确度，在众包资源方面，评估1000items仅需15-25个工人工作一个小时。

### 众包与其他问题
#### 众包与实体融合
■	S. Euijong Whang，P. Lofgren and H. Garcia-Molina. Question Selection for Crowd Entity Resolution. VLDB, 2013.  
针对实体融合（Entity Resolution）[10]对于计算机来说较难问题，斯坦福教授Hector及其团队提出利用众包解决实体融合，传统的实体融合过程分为两个部分Pairwise Analysis(获得的是records对的相似值)和Global Analysis(输出是最终结果，即属于同一实体的记录的集合)，而Hector团队将Pairwise Analysis中获得的结果抽取出来以二元问题的方式询问众包工人，其中其创新点在于提出probabilistic framework，用来1.估计问每个问题得到多少ER精度；2.选择有最高期望精度的问题作为用来问的问题（这里的每个问题对应于前面的records对）。目标是选择尽可能少的问题，并获得高准确度。本文将Crowd ER算法分别在合成数据和真实数据上进行了测试，证明该算法确实在有效减少问题数量的同时获得了高准确度。
#### 众包与Data Labeling
■    H.Hu, Y.Zheng, Z.Bao, G.Li, J.Feng and R.Cheng.  Crowdsourced POI Labelling: Location-Aware Result Inference and Task Assignment. In ICDE.2016, 2016    
Guoliang Li的团队使用众包的方式来解决为POI( points of interest)打标签的问题[3]。众包给POI打标签还有以下难点：首先，与普通的标签相比，POI标签有着更复杂的影响因素，有名的POI会得到更高质量的回答；其次，工人与POI的距离会影响工人的质量；最后，工人是动态进入答题的，很难立即识别工人的能力并明确地分配任务。提出一个框架包括推测模型inference model和在线任务分配器online task assigner。推测模型首先根据工人的固有质量将工人分成两类，高质量工人在结合他的距离感知质量和POI的影响加权得出工人准确率，推测模型使用Graphical Probability Model来推理答案，使用EM算法推算参数。通过在真实的众包平台上对两个真实数据的实验，推测模型与MV和EM方法比较，分配器与random和SF (Spatial-First assignment algorithm)算法比较，结果显示此方法效果更佳。

■	D.Haas, J.Wang, E.Wu and M.J.Franklin. CLAMShell: Speeding up Crowds for Low-latency Data Labeling. VLDB, 2015, 2015.    
Daniel Haas的团队在解决data labeling延时问题上也引入了众包[2]。Data labeling在数据分析中扮演着重要的作用，但其缓慢的过程阻碍了现代数据分析中交互系统的发展，因为manual labeling的延时性很高。因此Haas的团队提出了实现低延时的加速众包加速的系统，称之为CLAMShell。CLAMShell将延时分为三类，即per-task latency, batch-wise latency和end-to-end overall latency，并且使用Straggler mitigation, Pool maintenance,Hybrid learning和众包相结合的方法来解决三类data labeling延时问题。通过模拟和在Amazon的Mechanical Turk平台的在线实验，验证了CLAMShell在data labeling的准确率上实现了8倍加速。

■	S. Hao, S.C.H .Hoi, C. Miao and P. hao. Active Crowdsourcing for Annotation. IEEE Computer Society2015, 2015.    
南洋理工的Shuji Hao和Chunyan Miao等教授提出了一种通过众包的方式来获取数据标签的方法[8]。通过众包获取数据标签主要的挑战是存在给出错误答案的工人和问题提出者有限的预算资金。针对这样的问题本文提出了一种learning with expert的框架，通过这个框架可以从工人中找出准确率较高的工人，还提出了eliability-based allocation的方法，通过这个方法根据工人的可靠性来分配任务从而降低预算。通过在台湾国立大学的模拟数据集上进行实验，分别从不同的噪声环境中和其他方法进行对比，结果显示本文的方法在高错误率工人数量增加时，得出结果的准确率没有明显的下降。  


[1] D.Haas, J.Ansel, L.Gu and A.Marcus. Argonaut: Macrotask Crowdsourcing for Complex Data Processing. VLDB, 2015, 2015.    
[2] D.Haas, J.Wang, E.Wu and M.J.Franklin. CLAMShell: Speeding up Crowds for Low-latency Data Labeling. VLDB, 2015, 2015.  
[3] H.Hu, Y.Zheng, Z.Bao, G.Li, J.Feng and R.Cheng.  Crowdsourced POI Labelling: Location-Aware Result Inference and Task Assignment. In ICDE.2016, 2016  
[4] K.Mo, E.Zhong and Q.Yang. Cross-Task Crowdsourcing. KDD’13, August 11–14, 2013  
[5] F.Ma, Y.Li, Q.Li, M.Qiu, J.Gao, S.Zhi,L.Su, B.Zhao, H.Ji, and J.Han. FaitCrowd: Fine Grained Truth Discovery for Crowdsourced Data Aggregation. KDD’15, August 10-13, 2015.  
[6] A.D.Sarma, A.Parameswaran,J.Widom. Towards Globally Optimal Crowdsourcing Quality Management: The Uniform Worker Setting. SIGMOD’16, June 26-July 01, 2016.  
[7]A.Parameswaran, S.Boyd, H.Garcia-Molina, A.Gupta, N.Polyzotis and J.Widom. Optimal Crowd-Powered Rating and Filtering Algorithms. Proceedings of the Vldb Endowment 2014, 2014  
[8] S. Hao, S.C.H .Hoi, C. Miao and P. hao. Active Crowdsourcing for Annotation. IEEE Computer Society2015, 2015  
[9] P. Cheng, X. Lian, Z. Chen, R. Fu, L. Chen, J. Han and J. Zhao. Reliable Diversity-Based Spatial Crowdsourcing by Moving Workers. VLDB Endowment 2014, 2014  
[10] S. Euijong Whang，P. Lofgren and H. Garcia-Molina. Question Selection for Crowd Entity Resolution. VLDB, 2013.  
[11]C. Sun, N. Rampalli , F. Yang and A. Doan. Chimera: Large-Scale Classiﬁcation using Machine Learning, Rules, and Crowdsourcing. VLDB, 2014.  
[12] C. Cao, J. She, Y. Tong and L. Chen. Whom to Ask? Jury Selection for Decision Making Tasks on Micro-blog Services. VLDB，2012.  

## 2.	移动众包  
### 任务分配
	Online Mobile Micro-Task Allocation in Spatial Crowdsourcing  
In this paper, to address the shortcomings of existing offline approaches, we first identify a more practical micro-task allocation problem, called the Global Online Micro-task Allocation in spatial crowdsourcing (GOMA) problem. We first extend the state-of-art algorithm for the online maximum weighted bipartite matching problem to the GOMA problem as the baseline algorithm.
这篇论文针对的是动态环境中的任务分配，即工人和任务都是随机到达平台，平台对这些随到达的任务的工人进行匹配，提出TGOA algorithm-Greedy算法，目的是把任务分配给合适的工人，使得被分配的任务数量和工人-任务对的总权重最大。工人-任务对的权重等于工人完成任务的概率与该任务的报酬的乘积。TGOA algorithm-Greedy根据历史记录将一天分为若干时间段，每个时间段作为一个周期来进行任务分配。例如每1个小时作为一个时间段，那前半个小时采取贪心算法，后半个小时采取另一种算法。这样做技能保证分配的任务数量多，也可以做到总体权重最大。

	Kazemi, S.: GeoCrowd: enabling query answering with spatial crowdsourcing. In: SIGSPATIAL, pp. 189–198(2012)  
They define a taxonomy for spatial crowdsourcing (Figure 1). First, they classify spatial crowdsourcing based on people’s motivation. Next, they define two modes of task publishing in spatial crowdsourcing. Finally, they define two ways for spatial task assignment in spatial crowdsourcing.

	Truth Discovery in Crowdsourced Detection of Spatial Events  
The credibility of those detected events can be negatively impacted by unreliable participants with low-quality data. Consequently, a major challenge in quality control is to discover true events from diverse and noisy participants’ reports. This truth discovery problem is uniquely distinct from its online counterpart in that it involves uncertainties in both participants’ mobility and reliability. Decoupling these two types of uncertainties through location tracking will raise severe privacy and energy issues, whereas simply ignoring missing reports or treating them as negative reports will significantly degrade the accuracy of the discovered truth. In this paper, we propose a new method to tackle this truth discovery problem through principled probabilistic modeling.
We propose FMC TA, a novel task allocation algorithm that allows tasks to be easily sequenced to yield high-quality solutions. FMC TA first finds allocations that are fair (envyfree), balancing the load and sharing important tasks between agents, and efficient (Pareto optimal) in a simplified version of the problem. It computes such allocations in polynomial or pseudo-polynomial time (centrally or distributedly, respectively) using a Fisher market with agents as buyers and tasks as goods.  
目标：寻找能够实现团队最大效益的分配方式
本文所做工作：
1)	提出LEP问题（Law Enforcement Problem）。
此处举例警察局工作，警察要进行日常巡逻和对报警事件的处理，报警事件有不同的重要性和工作量。报警随时可能出现，那警察的分配方式必须是动态的，有时候必须中断一个事件的处理转而去处理其他事件。LEP问题就是寻找能实现团队最大效益的分配方式，不仅仅是警察局分配问题。
2)	提出FMA_TA，一个能产生高效解决方案的任务分配算法。
首先，FMC_TA先忽略时空限制和代理间的约束，通过简化的问题模型找到一种分配方式。然后，根据完整的问题模型，安排每个代理的任务执行顺序。
3)	解决给分配排序，产生高质量的解决方案的问题：
假设每个代理之间不会争夺任务，优先把重要的任务分配给质量高的代理，任务的分配执行按重要性排序，如果需要多个代理合作完成一项任务，必须所有代理都到达在能开始执行任务，在所有代理全部到达之前，在不会耽误该任务的情况下，就先安排该任务后面的任务执行。

	Multi-Agent Task Assignment for Mobile Crowdsourcing under Trajectory Uncertainties —AAMAS 2015  
现在移动众包的行业惯例是用户手动浏览、筛选任务，本文针对这个现象提出push-based模型，该模型使基于工人的历史记录，在考虑到时间预算的前提下为用户推荐任务。Push-based模型能够避免超级代理现象，即小部分工人完成大部分任务的现象。研究发现，超级代理的特点就是更乐意选择与自己的路由路线相近的任务。本文的思想是假设每个众包工人的轨迹具有不确定性，每个工人的路由路线列表是有限的，并且有已知的概率分布。  

	GeoCrowd: Enabling Query Answering with Spatial Crowdsourcing—SIGSPATIAL 2012   
文章定义了一个MTA（Maximum Task Assignment）问题，即最大任务分配问题。在一段时间内，requester像服务器发送SC-query，包含任务及任务可以由几个工人完成；每个准备好的工人给服务器发task-query，task-query包括工人工作的区域和他最大可以接受的任务数，服务器根据这两个query，来分配工作，使分配给工人的任务既能满足工人提出的要求，又能使分配的整体任务数达到一个最大。
文章该问题转换为图的最大流问题，用Ford-Fulkerson算法算出最大流。
实验通过Gowalla，一个社交网络平台收集的南加州某个地方工人的签到数据，签到即代表该工人完成了任务，实验设置了50k到200k的任务，每个任务的持续时间为40天，工人的最大接受任务数从1增加到20。工人的任务区域大小从0.01增加到0.05。
通过收集的数据验证了方法的可行性，实现了任务的最大化分配。  

	Maximum Complex Task Assignment: Towards Tasks Correlation in Spatial Crowdsourcing- iiWAS  ACM 2013  
文章自定义了一个复杂的任务分配问题Maximum Complex Task Assignment（MCTA），复杂任务是指包含很多子任务，这些子任务相互之间有关联。例如：其中一个人想获得十张某个特定建筑物的不同照片，他需要所有的这些照片，不能缺失任何一张，只能将这个任务分配给一个工人，否则获得的所有其他建筑物的照片是没用的，即这些照片是相互关联的，不能丢失任何一张。文章想实现在符合工人的约束下,把尽可能多的复杂任务分配给工人。
文章将实现最大复杂任务的分配问题转化为图的最大流问题，利用图的知识解决
实验通过Yelp收集的数据，Yelp是一个社交网络，致力于为本地企业的咨询服务和评论网站，将网站上用户作为工人，企业当作空间任务，同一个类别的企业当作一个复杂的空间任务，评价一个企业代表完成任务。第一个实验评估方法的可扩展性，选择工人1500，复杂任务数从1000到4000。结果表明，随着复杂任务数量的增加，整体分配增多；第二个实验查看工人数量对整体分配的影响，固定复杂任务数量为10000，工人的数量从250到4000。

	A Server-Assigned Spatial Crowdsourcing Framework-Hien To, Cyrus Shahabi  
文章定义了一个MTA（Maximum Task Assignment）问题，即最大任务分配问题。在一段时间内，requester像服务器发送SC-query，包含任务及任务可以由几个工人完成；每个准备好的工人给服务器发task-query，task-query包括工人工作的区域和他最大可以接受的任务数，服务器根据这两个query，来分配工作，使分配给工人的任务既能满足工人提出的要求，又能使任务数达到一个最大。
MTA问题假设多有任务的类型和工人质量是一样的，不符合实际，接着文章又定义了MSA（Maximum Score Assignment），最高分数分配，就是通过任务的类型把它分配给更适合这个任务的工人，例如，一个获得高质量照片的任务分配给摄像师。
MTA转换为寻找图的最大流问题，MSA转换为寻找图的最大加权二分匹配问题
实验通过Gowalla and Yelp两个社交网站收集的签到数据。

	GeoTruCrowd: Trustworthy Query Answering with Spatial Crowdsourcing—SIGSPATIAL 2013  
文章定义一个Maximum Correct Task  Assignment，最大正确任务分配，就是从潜在的匹配集里选择一个最好的匹配，潜在的匹配集（t,<wi，wj...>）是指给定一个任务和一组工人，只要工人的荣誉分大于任务的置信水平，就匹配工人和这个任务。工人的荣誉分是通过一个公式得到,在[1]中。每一个空间任务都应该被分配到足够多的工人，使他们的总信誉满足任务的置信水平。文章假设工人的荣誉分服务器知道并保存，所有任务都是同等难度的。
提出了几个启发式算法解决这个问题。第一个是贪心算法，第二个是本地优化算法，第三个是基于启发式的贪心算法。
实验是用Gowalla收集的签到数据，任务定义为去加利福尼亚不同的spots（例如餐馆）签到，对于每个签到，位置和签到的时间分别为任务的位置和完成时间，在不同的地点签到说明他完成了他自己附近的任务，对于工人的荣誉分和任务的置信水平随机从0到1之间选
[1]C. C. Cao, J. She, Y. Tong, and L. C. 0002. Whom to ask? jury selection for decision making tasks on micro-blog services. PVLDB’12, 5(11):1495–1506.
任务获取（Worker自行选择任务）

	Deng, C.S, Ugur.: Maximizing the Number of Worker’s Self-Selected Tasks in Spatial Crowdsourcing. In: SIGSPATIAL, pp.314-323(2013)  
In this paper, we study a version of the spatial crowdsourcing problem in which the workers autonomously select their tasks, called the worker selected tasks (WST) mode. Towards this end, given a worker, and a set of tasks each of which is associated with a location and an expiration time, we aim to find a schedule for the worker that maximizes the number of performed tasks.
文章基于Worker Selected Tasks (WST)工人选择任务这个模型，目标是想让工人选择的任务完成的数量最大限度的提高。提出了Maximum Task Scheduling (MTS)问题，解决的方法是想找到一个时间表，时间表要考虑到旅行成本及任务到期的时间两个因素，最大限度地提高任务的数量。时间表就是服务器给工人一个有效的任务序列，这个有效的任务序列是指按照这个顺序，这些任务都可以完成，即工人到达时间小于等于任务的最后期限。
文章解决的办法就是给定一个工人和在他可接受任务地域的范围内n个任务，通过动态规划和分支定界算法找到最长的有效任务序列。 
实验是用Gowalla收集的一个月内的签到数据，任务定义为去洛杉矶某餐馆签到，工人在一个时间范围内去这个餐馆签到即代表完成了任务。对于每个签到，餐馆的位置和签到的时间分别为任务的位置和完成时间。通过实验证明他的方法可以有效提高分配的任务数量。

	Oriented Online Route Recommendation for Spatial Crowdsourcing Task Workers  
In this paper, we study the problem of online recommending an optimal route for a crowdsourcing worker, such that he can (i) reach his destination on time and (ii) receive the maximum reward from tasks along the route.

	Location-based crowdsourcing: extending crowdsourcing to the real world  
In this paper we assess how the idea of user-generated content, web-based crowdsourcing, and mobile electronic coordination can be combined to extend crowdsourcing beyond the digital domain and link it to tasks in the real world. To explore our concept we implemented a crowdsourcing platform that integrates location as a parameter for distributing tasks to workers. In the paper we describe the concept and design of the platform and discuss the results of two user studies.


### 路径规划
	Oriented Online Route Recommendation for Spatial Crowdsourcing Task Workers  
In this paper, we study the problem of online recommending an optimal route for a crowdsourcing worker,  such that he can (i) reach his destination on time and (ii) receive the maximum reward from tasks along the route.   
当前已知的任务推荐方式是MTS(Maximum Task Scheduling)，能够返回一条包含最大任务数的路线，但是并不能考虑到任务的随机性，不会因为新任务的到达重新调整路线。本文提出的算法克服了两个问题：1）根据新发布的任务更新用户的路线；2）能够与用户自身的路线匹配，即工人有时候已经规划了自己的路线，到达某个目的地有自己的deadline，那任务分配必须考虑到用户的需求。

	Towards City-scale Mobile Crowdsourcing: Task Recommendations under Trajectory Uncertainties—ICJAI 2015  
现在的众包平台出现一个超代理现象，即一小部分人执行大部分的任务，而那些得不到超代理的普通工人由于没有足够的任务就选择退出不去执行任务了，这渐渐将会导致工人数量和平台容量的减少。在本篇文章中，在基于推送任务的移动众包平台下，根据工人日常的路线进行任务推荐，使每个工人都能选择适合自己路线的任务，不仅能够少走弯路，减少时间花费，还能够使更多的任务完成，推荐的任务也更均匀的分布。
在这篇文章中，没有考虑确定的模型，只研究随机的任务推荐，假设任务推荐问题是一个随机整数线性规划的问题，并假设每个工人的日常路线是已知的，轨迹列表是有限的，符合一个已知的概率分布，我们利用问题的结构，将问题分解为agent-specific routing 子问题，每一个子问题都可以利用拉格朗日松弛法有效地解决。
安全与隐私

	Crowdsourcing Spatial Phenomena Using Trust-Based Heteroskedastic Gaussian Processes  
In this context, we propose a new spatial function modelling approach to address the problem of fusing multiple spatial observations reported by possibly untrustworthy users in the domains of participatory sensing and crowdsourcing applications. Specifically, we use a heteroskedastic Gaussian process model to incorporate user trust modelling into Bayesian spatial regression. In particular, by training the model with the reports gathered from the crowd, we are able to estimate the spatial function at any location of interest and also learn the level of trustworthiness of each user

	PrivGeoCrowd: A toolbox for studying private spatial Crowdsourcing – ICDE 2015  
Protecting location privacy is an important concern in SC, as an adversary with access to individual whereabouts can infer sensitive details about a person (e.g., health status, political views). Due to the challenging nature of protecting worker privacy in SC, solutions for this problem are quite complex, and require tuning of several parameters to obtain satisfactory results. In this paper, we propose PrivGeoCrowd, a toolbox for interactive visualization and tuning of SC private task assignment methods. This toolbox is useful for several real-world entities that are involved in SC, such as: mobile phone operators that want to sanitize datasets with worker locations, spatial task requesters, and SC-service providers that match workers to tasks.

	A Framework for Protecting Worker Location Privacy in Spatial Crowdsourcing  
In this paper, we introduce a framework for protecting location privacy of workers participating in SC tasks. We argue that existing location privacy techniques are not sufficient for SC, and we propose a mechanism based on differential privacy and geocasting that achieves effective SC services while offering privacy guarantees to workers.

	Truth Discovery in Crowdsourced Detection of Spatial Events  
The credibility of those detected events can be negatively impacted by unreliable participants with low-quality data. Consequently, a major challenge in quality control is to discover true events from diverse and noisy participants’ reports. This truth discovery problem is uniquely distinct from its online counterpart in that it involves uncertainties in both participants’ mobility and reliability. Decoupling these two types of uncertainties through location tracking will raise severe privacy and energy issues, whereas simply ignoring missing reports or treating them as negative reports will significantly degrade the accuracy of the discovered truth. In this paper, we propose a new method to tackle this truth discovery problem through principled probabilistic modeling.

	Towards Globally Optimal Crowdsourcing Quality Management: The Uniform Worker Setting  
In this paper, we focus on filtering, where tasks require the evaluation of a yes/no predicate, and rating, where tasks elicit integer scores from a finite domain. We design algorithms for finding the global optimal estimates of correct task answers and worker quality for the underlying maximum likelihood problem, and characterize the complexity of these algorithms.

### SC平台、原型系统
	gMission: A General Spatial Crowdsourcing Platform  
In this demo, we will introduce gMission, a general spatial crowdsourcing platform, which features with a collection of novel techniques, including geographic sensing, worker detection, and task recommendation.

	Towards a Generic Framework for Trustworthy Spatial Crowdsourcing-- MobiDE   2013  
文章主要介绍了一个移动众包的框架，GeoCrowd由两个主要部分组成：一个SC-server和一个移动客户端。服务器将使大众发表自己的空间众包请求（利用地图界面），然后，这些请求被系统翻译成一系列的空间任务。移动客户端，工人在他们的手机上下载客户端，查找任务并去执行。这篇文章是一个demo，没有讲具体的实现，只说明了众包需要扩大规模，能够应用到对社会有重大影响的社会领域，比如救灾时的灾后重建。这篇文章的可用性很小。

	improving the Performance of Mobile Phone Crowdsourcing Applications—AAMAS 2015  
文章介绍提高了一个关于众包的手机应用程序kpark的性能，更好的预测停车场的停车位。应用程序通过可信的数据融合技术来提高用户提交的停车报告的质量。我认为这篇文章没太有用，只是讲了提高了手机app的性能，众包体现的不是很明显。


### 众包数据整合
	Crowdsourcing Spatial Phenomena Using Trust-Based Heteroskedastic Gaussian Process  
本文的目的是整合众包平台上收集到的数据。因为通过众包获取的数据可能是不可靠的，可能因为用户的传感设备出错，或者有用户恶意的行为，即用户的可信度不确定。提出了HGP模型。

### 激励机制
	A Truthful Online Auction for Tempo-spatial Crowdsourcing Tasks  
现在很多激励机制都是假设移动众包平台的任务是静态的，即使是考虑到任务动态性的研究，大多数都忽略了传感任务的一些重要的因素（不考虑任务的位置信息；没有考虑到任务和工人都是随机到达的事实；暴露了工人位置、工人为了完成任务所用时间、金钱等隐私；没有考虑到用户会为了自身收益擅自做出自己的选择的情况）。
本文的贡献是 在设计激励机制的时候，同时考虑到了任务和用户的时间、位置因素。具体做法分为两步：1）选择工人2）为工人计算报酬 
复杂任务

	CrowdWeaver : Visually Managing Complex Crowd Word   
本文中提出CrowdWeaver，一个提供可视化界面来管理复杂众包任务的系统。现在大多数众包平台针对的是简单、相互独立的任务，虽然已经有一些工具、平台支持更复杂的任务和工作流，但是在管理工作流方面有很大缺陷。本问所提出的系统就能够管理复杂任务的工作流。

	CrowdForge : Crowdsourcing Complex Work  
通过MTurk(Amazon’s Mechanical Turk)只能完成复杂度低、相互独立、所需的时间少、对工人的认知成都没有要求的任务。但是现实中有很多任务是更复杂的、互相依赖的并且需要一定的时间，对工人的专业技术也有要求，这类任务的完成需要工人间相互合作、协调。例如，写一篇文章。本文针对这样复杂的任务，在基于MTurk这样的微任务平台，提出CrowdForge系统，能够将复杂任务分割成子任务并且能够管理子任务之间的执行顺序和依赖性。本文中心思想是将复杂任务分为三种类型，针对不同类型的复杂任务提出不同的分割方式。  

[1] Y.Tong, J.She, B.Ding, L.Wang, L.Chen. Online Mobile Micro-Task Allocation in Spatial. ICDE, 2016, 2016  
[2] L.Kazemi , C. Shahabi.GeoCrowd: Enabling Query Answering with Spatial  
Crowdsourcing. ACM SIGSPATIAL GIS ’12 , 2012  
[3] Robin Wentao Ouyang and A.Toniolo. Truth Discovery in Crowdsourced Detection of Spatial Ecents, CIKM’14 , 2014.  
[4] Sofia Amador, Steven Okamoto, Roie Zivan.Dynamic Multi-Agent Task Allocation with Spatial and Temporal Constraints. AAAI, 2014.  
[5] Cen Chen, Shih-Fen Cheng, Archan Misra, Hoong Chuin Lau. Multi-Agent Task Assignment for Mobile Crowdsourcing under Trajectory Uncertainties. AAMAS, 2015.  
[6] Yu Li, Man Lung Yiu, Wenjian Xu. Oriented Online Route Recommendation for Spatial Crowdsourcing Task Workers. SSTD, 2015.  
[7] Matteo Venanzi, Alex Rogers, Nicholas R. Jennings.  Crowdsourcing Spatial Phenomena Using Trust-Based Heteroskedastic Gaussian Process. AAAI, 2013  
[8] Yue Fan, Hailong Sun, Yanmin Zhu, Xudong Liu, Ji Yuan.  A Truthful Online Auction for Tempo-spatial Crowdsourcing Tasks. IEEE, 2015.  
[9] Aniket Kittur, Susheel Khamkar, Paul Andre, Robert E. Kraut. CrowdWeaver : Visually Managing Complex Crowd Word. CSCW, 2012.  
[10] Aniket Kittur, Susheel Khamkar, Paul Andre, Robert E. Kraut. CrowdForge : Crowdsourcing Complex Work. UIST, 2011.  
[11] Robin Wentao Ouyang ,Alice Toniolo. Truth Discovery in Crowdsourced Detection of Spatial Events. CIKM , 2014  
[12] Leyla Kazemi , Cyrus Shahabi. GeoCrowd: Enabling Query Answering with Spatial Crowdsourcing. ACM SIGSPATIAL, 2012  
[13] Cyrus Shahabi, Towards a Generic Framework for Trustworthy Spatial Crowdsourcing, MobiDE , 2013.  
[14] Erfan Davami, Gita Sukthankar, Improving the Performance of Mobile Phone Crowdsourcing Applications, AAMAS, 2015.  
[15] Hung Dang, Tuan Nguyen，Hien To, Maximum Complex Task Assignment: Towards Tasks Correlation in Spatial Crowdsourcing, iiWAS, 2013.  
[16] Hien To , Gabriel Ghinita , Cyrus Shahabi, PrivGeoCrowd: A Toolbox for Studying Private Spatial Crowdsourcing, ICDE, 2015.  
[17] Dingxiong Deng, Cyrus Shahabi, Ugur Demiryurek, Maximizing the Number of Worker’s Self-Selected Tasks in Spatial Crowdsourcing, SIGSPATIAL, 2013.  
[18] Cen Chen, Shih-Fen Cheng, Hoong Chuin Lau, Archan Misra, Towards City-scale Mobile Crowdsourcing: Task Recommendations under Trajectory Uncertainties, ICJAI 2015.  
[19] Hien To, Cyrus Shahabi, Leyla Kazemi, A Server-Assigned Spatial Crowdsourcing Framework  
[20] Leyla Kazemi, Cyrus Shahabi, Lei Chen, GeoTruCrowd: Trustworthy Query Answering with Spatial Crowdsourcing, SIGSPATIAL, 2013.  
