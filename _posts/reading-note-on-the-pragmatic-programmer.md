title: Reading Note on The Pragmatic Programmer
date: 2013-12-08 08:12:03
tags:
 - reading
---

《程序员修炼之道》阅读笔记
============================================

###本书的阅读感受

  * 内容浅显易懂、但有些道理需要实践才能真正领悟
  * 书脊不结实，容易掉页
  * 翻译质量打75分，基本通顺，具体问题见下文
<!-- more -->

###书中推荐的几本书

  * 《Unix编程艺术》（准备看）
  * 《代码大全2》（正在看）
  * 《卓有成效的程序员》（评估后再决定）
  * 《Elements of Programming Style》（要看，[推荐语](http://blog.youxu.info/2008/11/23/the-elements-of-programming-styl/)）
  * 《Large-Scale C++ Software Design》 （待评估）
  * 《算法》（已买，有空看）
  * 《重构》 （重读）
  * 《Object Oriented Software Construction, 2nd edition》 （太厚，太基础，要读吗？1300多页）
  * 《设计模式》（重读）
  * 《分析模式》（检查是否在书库）
  * 《Dynamics of Software Development》（文章，可读）
  * 《Effective Java》（要读）

###书中作序的两位优质程序员的Blog

  * [徐宥的博客](http://blog.youxu.info/)
  * [云风的博客](http://blog.codingnow.com/)

###书中的一些点滴

在**重复的危害**中提到，系统中的每一项知识都必须具有单一、无歧义、权威的表示。重复是怎样发生的中给出了四种重复的分类：

  * 强加的重复

	  * 信息的多种表示
	  * 代码中的文档

		  * 糟糕的代码才需要许多注释
		  * DRY法则告诉我们，要把低级的知识放在代码中，把注释保留给高级的说明

	  * 文档与代码
	  * 语言问题

  * 无意的重复
  * 无耐性的重复
  * 开发者之间的重复。

**EJB3.1**还是值得一看的，抽时间详细了解一下。

“**线程安全**”比较简单易懂的解释见[维基百科](http://zh.wikipedia.org/wiki/%E7%BA%BF%E7%A8%8B%E5%AE%89%E5%85%A8)

**黑板模型**的参考JavaSpaces，需要了解主要用处：[1](http://www.dancres.org/cottage/javaspaces.html)，[2](http://www.oracle.com/technetwork/articles/javase/javaspaces-140665.html)

>测试是技术，但更是文化。不管所用语言是什么，我们都可以让这样的测试文化慢慢渗入项目中。

>作为开发者，你在整个职业生涯中都在做同样的事情。你一直在试验各种东西，看哪些可行，哪些不可行。你一直在积累经验与智慧。当你面对一件任务时，如果你反复感觉到疑虑，或是体验到某种勉强，要注意它。你可能无法准确地指出问题所在，但给它时间，你的疑虑很可能就会结晶成某种更坚实的东西，某种你可以处理的东西。软件开发仍然不是科学。让你的直觉为你的表演做出贡献。

>注重实效的程序员批判地看待方法学，并从各种方法学中提取精华，融合成每个月都在变得更好的一套工作习惯。这至关重要。你应该不断努力提炼和改善你的开发过程。决不要把方法学的呆板限制当作你世界的边界。

Test **State Coverage**, not Code Coverage 这一条确实第一次知道，查阅网络，有相关的论文如下，需要学习一下，[1](http://research.microsoft.com/pubs/164422/StateCoverage.pdf)，[2](http://www-cs-students.stanford.edu/~kkoster/pubs/statecoverage.pdf)

###Tips汇总

官方网站有所有的[Tips](http://pragmatictips.com/)，并且每一个Tip都有一小段解释，很不错，下面用列表的形式汇总一下，以便搜索查阅。

	1. Care About Your Craft
	2. Think! About Your Work
	3. Provide Options, Don't Make Lame Excuses
	4. Don't Live with Broken Windows
	5. Be a Catalyst for Change
	6. Remember the Big Picture
	7. Make Quality a Requirements Issue
	8. Invest Regularly in Your Knowledge Portfolio
	9. Critically Analyze What You Read and Hear
	10. It's Both What You Say and the Way You Say it
	11. DRY - Don't Repeat Yourself
	12. Make It Easy to Reuse
	13. Eliminate Effects Between Unrelated Things
	14. There Are No Final Decisions
	15. Use Tracer Bullets to Find the Target
	16. Prototype to Learn
	17. Program Close to Problem Domain
	18. Estimate to Avoid Surprises
	19. Iterate the Schedule with the Code
	20. Keep Knowledge in Plain Text
	21. Use the Power of Command Shells
	22. Use a Single Editor Well
	23. Always Use Source Code Control
	24. Fix the Problem, Not the Blame
	25. Don't Panic
	26. "Select" Isn't Broken
	27. Don't Assume It - Prove It
	28. Learn a Text Manipulation Language
	29. Write Code That Writes Code
	30. You Can't Write Perfect Software
	31. Design with Contracts
	32. Crash Early
	33. If It Can't Happen, Use Assertions to Ensure That It Won't
	34. Use Exceptions for Exceptional Problems
	35. Finish What You Start
	36. Minimize Coupling Between Modules
	37. Configure, Don't Integrate
	38. Put Abstractions in Code, Details in Meta-data
	39. Analyze Workflow to Improve Concurrency
	40. Design Using Services
	41. Always Design for Concurrency
	42. Separate Views from Models
	43. Use Blackboards to Coordinate Workflow
	44. Don't Program by Coincidence
	45. Estimate the Order of Your Algorithms
	46. Test Your Estimates
	47. Refactor Early, Refactor Often
	48. Design to Test
	49. Test Your Software, or Your Users Will
	50. Don't Use Wizard Code You Don't Understand
	51. Don't Gather Requirements - Dig for them
	52. Work with a User to Think Like a User
	53. Abstractions Live Longer than Details
	54. Use a Project Glossary
	55. Don't Think Out of Box - Find the Box
	56. Listen to Nagging Doubts - Start When You're Ready
	57. Some Things Are Better Done than Described
	58. Don't Be a Slave to Formal Methods
	59. Expensive Tools Do Not Produce Better Designs
	60. Organize Around Functionalities, Not Job Functions
	61. Don't Use Manual Procedures
	62. Test Early. Test Often. Test Automatically.
	63. Coding Ain't Done 'Til All the Tests Run
	64. Use Saboteurs to Test Your Testings
	65. Test State Coverage, not Code Coverage
	66. Find Bugs Once
	67. Treat English as Just Another Programming Language
	68. Build Documentation In. Don't Bolt It On
	69. Gently Exceed Your Users' Expectations
	70. Sign Your Work

###一些翻译不当的地方

  * 总体上，行文还算通顺，有些地方比较拗口，质量有改进空间。
  * P13：古鲁（Guru），这样翻译有一些宗教的意味，在技术书籍里读起来有点怪，不如翻译成“大师”。Guru字典里有”上师”、“导师”、“大师”、“专家”、“领袖”和“古鲁”的译法，在计算机领域，一般Guru指的是个人能力很强、有思想和见地、在社区里享有盛誉的专家（行家），因为专家过于正式化，还是使用“大师”比较好。
  * P29： 远地访问，此处应为“远程访问”，原文应该是remote。
  * P34： “中流换马（Change horse in midstream）”：中文应该没有这个成语，查阅词典，可以选择“中途改变策略”。英文中的习语不见得要直译照搬。参考翻译：

	  * 中途改变策略
	  * 临阵换将
	  * 中途换马，中途改变计划
	  * 在危急中作出重大的变动

  * P43： 遮蔽特定的解决方案，这个不通，原文是Cover吗？如果是的话，可以译成“涵盖”、“包含”或“涉及”。
  * P46： screen scraping 翻译成“刮屏”？翻译成“屏幕抓取”更好 
  * P78： flat翻译成“平板”，不正确，可以译为“平面文件”
  * P87： precondition和postcondition翻译成前置条件、后置条件较好
  * P89： method signature 翻译成“方法型构”？中文里没这个词吧，还不如“签名”好，可能有更好的翻译方法
  * P92： policiy 拼写错误
  * P111： Law of Demeter 一般翻译成“迪米特法则”
  * P115： “折中”，还是“折衷”，是不是太随意了？
  * P117： “软和”，是不是“柔软”更合适？
  * P119： 商业逻辑， 一般翻译成业务逻辑
  * P173： 做活路？
  * P177： 规范如果翻译自Spec，可以译成“说明”，规范一般是Convention




