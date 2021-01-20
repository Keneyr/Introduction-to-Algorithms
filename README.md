# Introduction-to-Algorithms

学习《算法导论》并进行思考总结及C++实现

关于C++ STL的内部Data Structure和Algorithms，移步去看我的STLAnalysis Repo

如果有时间，再来更《算法导论》中的习题以及对各种证明的思考...

## 第10章 基本数据结构

### 10.1 栈和队列

有关**栈**的几种操作伪代码如下：

(以数组来实现)

```
STACK-EMPTY(S)
	if top[S] = 0
		then return TRUE
		else return FALSE
		
PUSH(S,x)
	top[S]<-top[S]+1
	S[top[S]]<-x

POP(S)
	if STACK-EMPTY(S)
		then error"underflow"
		else top[S]<-top[S]-1
			return S[top[S]+1]
```

有关**队列**的几种操作伪代码如下：

(以数组来实现，在最后一个位置，要进行“卷绕”，即队列中的n个元素排成环形，位置1接在位置n之后~)

(想起来侯捷老师在讲队列的时候，说队列这里是怎么实现先进先出的呢？其实就是首尾相连)

```
ENQUEQUE(Q,x)
	Q[tail[Q]]<-x
	if tail[Q] = length[Q]
		then tail[Q]<-1
		else tail[Q]<-tail[Q]+1
		
DEQUEUE(Q)
	x<-Q[head[Q]]
	if head[Q] = length[Q]
		then head[Q]<-1
		else head[Q]<-head[Q]+1
	return x
```

C++中的栈Stack和队列Queue内部是用deque这个容器实现的，所以严格来讲C++中的Stack和Queue应该叫做适配器~

deque容器和vector容器很像，内部都是动态数组~
	
### 10.2 链表

双向链表特别重要，C++中的LIST容器内部就是一个双向链表~

有关**链表**的几种操作伪代码如下：

(链表有头指针)

```
LIST-SEARCH(L,k)
	x<-head[L]
	while x不等于NULL and key[x]不等于k
		do x<-next[x]
	return x

LIST-INSERT(L,x)
	next[x]<-head[L]
	if head[L]不等于NULL
		then prev[head[L]]<-x
	head[L]<-x
	prev[x]<-NULL
	
LIST-DELETE(L,x)
	if prev[x]不等于NULL
		then next[prev[x]]<-next[x]
		else head[L]<-next[x]
	if next[x]不等于NULL
		then prev[next[x]]<-prev[x]
```

### 10.3 指针和对象的实现

用数组来实现这个？没有兴趣，暂时不看...

## 第11章 散列表

C#中的Dictionary字典内部实现其实就是HashTable..

### 11.1 直接寻址表

大眼一瞅，感觉说了半天就是在说普通的数组啊...

### 11.2 散列表

用公式来讲就是，利用散列函数h，根据关键字k计算出槽的位置。

函数h将关键字域U映射到散列表T[0..m-1]的槽位上：

h:U-->{0,1,...,m-1}

由于|U|>m，故必有两个关键字其散列值相同，所以想要完全避免碰撞是不可能的。

解决碰撞的技术有**链接法(chaining)和开放寻址法**。

链接法：把散列到同一槽中的所有元素都放在一个链表中。槽j中有一个指针，它指向由所有散列到j的元素构成的链表的头；如果不存在这样的元素，则j中为NULL。

采用链接法解决碰撞后，散列表T上的字典操作就很容易实现。

```
CHAINED-HASH-INSERT(T,x)
	insert x at the head of list T[h(key[x])]
	
CHAINED-HASH-SEARCH(T,k)
	search for an element with key k in list T[h(k)]
	
CHAINED-HASH-DELETE(T,x)
	delete x from the list T[h(key[x])]
```

以上伪代码中，x表示元素，key(x)表示关键字~

### 11.3 散列函数

大多数散列函数都假定关键字域为自然数集N={0,1,2,...}，如果所给关键字不是自然数，则要有一种方法将它解释为自然数。

#### 除法散列法

通过取k除以m的余数，来将关键字k映射到m个槽的某一个中去，散列函数为：

h(k) = k mod m

m不应该是2的幂，可以选m的值是与2的整数幂不太接近的质数。

(至于原因我也解释不太清楚...)

#### 乘法散列法

第一步，用关键字k乘上常数A(0<A<1)，并抽取kA的小数部分。

第二步，用m乘以这个值，再取结果的底(floor)。公式表达就是：

h(k) = [m(kA mod 1]

乘法的优点是对m的选择没啥特别的要求，一般选择它为2的某个幂次~

(原因我也不解释了，因为我也还没看懂为啥，毕竟没有数学生那聪明的小脑袋瓜儿..)

#### 全域散列

随机的选择散列函数，使之独立于要存储的关键字。

(其他的没看懂,还要有数论知识.饶了我吧...)

### 11.4 开放寻址法

开放寻址法(open addressing)~

?

### 11.5 完全散列




## 第12章 二叉查找树

二叉查找树(binary search tree)其实就是最基本最简单的树了，在实际开发中，常用的是二叉树变种

比如红黑树/B树以及B+/B\*等

对于数据库MySQL工程师而言，B树尤其是B+树，是必须学会的东西~

### 12.1 二叉查找树

一般用链表来Coding...

中序遍历/前序遍历/后序遍历

中序遍历伪代码：

```
INORDER-TREE-WALK(x)
	if x 不等于 NULL
		then INORDER-TREE-WALK(left[x])
			 print key[x]
			 INORDER-TREE-WALK(right[x])
```

### 12.2 查询二叉查找树

#### 查找

给定指向树根的指针和关键字k，过程TREE-SEARCH返回指向包含关键字k的结点的指针；否则，返回NULL

```
TREE-SEARCH(x,k)
	if x == null or k = key[x]
		then return x
	if k<key[x]
		then return TREE-SEARCH(left[x],k)
		else return TREE-SEARCH(right[x],k)
```

在大多数计算机上，**非递归版本运行得要更快一些**。所以上面的伪代码可以改为：

```
ITERATIVE-TREE-SEARCH(x,k)
	while x 不等于 NULL and k 不等于 key[x]
		do if k<key[x]
			then x<-left[x]
			else x<-right[x]
```			











