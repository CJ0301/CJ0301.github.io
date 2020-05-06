---
layout: 		post
title: 			"设计模式"
subtitle: 		'设计模式思想'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
mermaid:        true
tags:
  - Computer Science
---

## 面向对象的溜达原则
#### 单一职责原则
单一职责原则的定义是：就一个类而言，应该仅有一个引起它变化的原因。简单来说，一个类应该是一组相关性很高的函数与数据的封装。

特点：
1. 降低类的复杂性。
2. 提高可读性。
3. 提高可维护性。
4. 降低变更引起的风险。

🌰：
当我们需要写一个DrawPicture类  
一般编写方式：
<div class="mermaid">
classDiagram
class DrawPicture{
    +drawCircle()
    +drawRect()
    +showCircle()
    +showRect()
}
</div>

单一职责原则：
<div class="mermaid">
classDiagram
	DrawPicture <|-- Draw
	DrawPicture <|-- show
	class Draw{
		+drawCircle()
    	+drawRect()
	}
	class show{
		+showCircle()
    	+showRect()
	}
</div>

重点：  
1. 接口一定要做到单一职责。
2. 类的单一职责比较难实现，尽量做到单一职责。
3. 一个方法尽可能做一件事，能分解就分解，分解到原子级别。

适用范围：类、接口、方法


#### 里氏替换原则
里氏替换原则的定义是：所有引用基类的地方必须能透明地使用其子类的对象。

里氏替换原则的核心原理是抽象，抽象又依赖于继承。  
继承的优点：  
1. 代码重用，减少创建类的成本，每个子类具有父类的方法和属性。 
2. 子类与父类基本相似，但又有区别。  
3. 提高代码的可拓展性。  
继承的缺点：  
1. 侵入性 : 继承是侵入性的, 子类 强制继承 父类的方法和属性;
2. 灵活性 : 降低代码的灵活性, 子类必须拥有父类的属性和方法, 子类收到了父类的约束, 这是从子类的角度讲得;
3. 耦合性 : 增强了耦合性, 父类的属性和方法被修改时, 还需要顾及其子类, 可能会带来大量的重构, 这是从父类的角度讲的;

注意点：
1. 父类的返回值类型必须大于子类返回值类型。
2. 避免让子类拥有自己的成员变量或方法，同时避免子类重载父类方法。

总结：里氏替代原则是为一类问题提供了指导原则，也就是建立抽象，通过抽象建立规范，同时在具体实现时替换抽象，保证系统的拓展性与灵活性。这样的思想能保证子类能够替换父类，体现了多态性。

