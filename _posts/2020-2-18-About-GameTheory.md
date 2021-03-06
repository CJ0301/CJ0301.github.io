---
layout: 		post
title: 			"博弈论的笔记整理"
subtitle: 		'之前就有对博弈论感兴趣，这次听耶鲁大学的网课颇有收获，故借此机会记点笔记'
author: 		"CJ"
header-img: 	"img/post-bg-gameThe.jpg"
outer-img:		"post-bg-gameThe.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Game Theory
---

## 先来一个小游戏
&emsp;这里有一个小游戏，每个人都有α和β两个选项，然后随机配对到另一个伙伴，选α的人遇到选β的人，则α的分数为3，对方为-1，如果选α的人遇到选α的人，则双方都为零分，如果都选了β，则各得一分。如下表所示：  
<table border="1px" style="border-collapse: collapse;">
        <tr>
            <td colspan="2" rowspan="2"></td>
            <td colspan="2" align="center">Others</td>
        </tr>
        <tr>
            <td align="center">α</td>
            <td align="center">β</td>
        </tr>
        <tr>
            <td rowspan="2" align="center">Me</td>
            <td align="center">α</td>
            <td align="center">(0,0)</td>
            <td align="center">(3,-1)</td>
        </tr>
        <tr>
            <td align="center">β</td>
            <td align="center">(-1,3)</td>
            <td align="center">(1,1)</td>
        </tr>
    </table>

&emsp;由这个表我们可以简单得出一个结论：无论对方选什么，我们选α的得分始终比选β的要高。 
   
&emsp;这里我们给他下个定义：无论别人做什么选择的情况下，如果选α得到的结果严格优于β，那么α相对于β是个```严格优势策略```。

&emsp;在上面这个游戏中，大多数人肯定会选择α。但是思考一下，如果游戏无限的进行下去，选β的人发现自己吃了亏，决定在之后的回合里都选α，那么游戏结果已经显而易见了，后面游戏的结果都是零分。而如果每个人都达成共识，都选了β，那么所有人都能得到加分(虽然收益不如欺骗他人)。

&emsp;由此我们又可以得到一个结论：理性人的理性选择会造成次优的结果。经济学上有个专业名词叫```帕累托效率```。

&emsp;这里举个🌰：  
&emsp;猎鹿博弈  
&emsp;在原始社会，人们靠狩猎为生。为了使问题简化，设想村庄里只有
帕累托最优
帕累托最优
两个猎人，主要猎物只有两种：鹿和兔子。如果两个猎人齐心合力，忠实地守着自己的岗位，他们就可以共同捕得一头鹿。要是两个猎人各自行动，仅凭一个人的力量，是无法捕到鹿的，但却可以抓住4只兔子。从能够填饱肚子的角度来看，4只兔子可以供一个人吃4天；1只鹿如果被抓住将被两个猎人平分，可供每人吃10天。也就是说，对于两位猎人，他们的行为决策就成为这样的博弈形式：要么分别打兔子，每人得4；要么合作，每人得10（平分鹿之后的所得）。如果一个去抓兔子，另一个去打鹿，则前者收益为4，而后者只能是一无所获，收益为0。在这博弈中，要么两人分别打兔子，每人吃饱4天；要么大家合作，每人吃饱10天，这就是这个博弈两个可能结局。<sup>[[1]](#ref1)</sup>

&emsp;现在假设有两类人，一种喜欢选α，另一种喜欢选β。面对第一类人，我们肯定会选择α。而面对第二类人时，我们可能还是会选择α来最优化我们的利益，或者选β实现共赢。  
&emsp;由此我们得出结论是：要站在别人的立场上分析他们会怎么做。

## 第二个游戏
我们讲表格改成如下形式：
<table border="1px" style="border-collapse: collapse;">
        <tr>
            <td colspan="2" rowspan="2"></td>
            <td colspan="2" align="center">Others</td>
        </tr>
        <tr>
            <td align="center">α</td>
            <td align="center">β</td>
        </tr>
        <tr>
            <td rowspan="2" align="center">Me</td>
            <td align="center">α</td>
            <td align="center">(0,0)</td>
            <td align="center">(-1,-3)</td>
        </tr>
        <tr>
            <td align="center">β</td>
            <td align="center">(-3,-1)</td>
            <td align="center">(1,1)</td>
        </tr>
    </table>

这里我们选α肯定不会比对方亏，但是没有赚。选β可能会赚，也可能会亏。这里就没有第一种游戏中的优势策略了。这便是博弈论中的```协和谬误```。
&emsp;这里举个🌰：   
&emsp;不能承受的代价  
&emsp;妈妈花2000元给亚莉买了一架电子琴，可亚莉生性好动，对音乐没有什么兴趣，电子琴渐渐落了灰。不久，亚莉妈妈的同事介绍说有一位音乐学院钢琴专业的老师可以给亚莉做家教。这个时候你觉得亚莉妈妈会做何决定呢？亚莉妈妈决定请家教，理由是：“电子琴都买了，当然要好好学，请一个老师教教，要不这个琴就浪费了！”于是，每月500元的付出又坚持了半年，最终不得不放弃了。为了不浪费2000元的电子琴，亚莉妈妈继续浪费了3000元的家教费。<sup>[[1]](#ref2)</sup>




## 总结
综上，我们总结出如下四个结论：
  
- 不要选择劣势策略  
- 理性导致次优结果  
- 学会换位思考  
- 想清楚你想得到什么    




引用链接：  

- <a id="ref1" href="https://baike.baidu.com/item/%E5%B8%95%E7%B4%AF%E6%89%98%E6%9C%80%E4%BC%98/1768788?fromtitle=%E5%B8%95%E7%B4%AF%E6%89%98%E6%95%88%E7%8E%87&fromid=3664561&fr=aladdin#1_3">[百度百科-猎鹿博弈]
- <a id="ref1" href="https://baike.baidu.com/item/%E5%8D%8F%E5%92%8C%E8%B0%AC%E8%AF%AF/1217416?fr=aladdin">[百度百科-不能承受的代价]

## 博弈组成要素
1. 参与人 players
2. 策略   strategy
3. 利益   payoff