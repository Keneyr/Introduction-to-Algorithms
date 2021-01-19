# Introduction-to-Algorithms

学习《算法导论》并进行思考总结及C++实现

关于C++ STL的内部Data Structure和Algorithms，移步去看我的STLAnalysis Repo

如果有时间，再来更《算法导论》中的习题...

## 第10章 基本数据结构

### 10.1 栈和队列

有关**栈**的几种操作伪代码如下：

(以数组来实现)

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

有关**队列**的几种操作伪代码如下：

(以数组来实现，在最后一个位置，要进行“卷绕”，即队列中的n个元素排成环形，位置1接在位置n之后~)

(想起来侯捷老师在讲队列的时候，说队列这里是怎么实现先进先出的呢？其实就是首尾相连)

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

C++中的栈Stack和队列Queue内部是用deque这个容器实现的，所以严格来讲C++中的Stack和Queue应该叫做适配器~

deque容器和vector容器很像，内部都是动态数组~
	
### 10.2 链表

双向链表特别重要，C++中的LIST容器内部就是一个双向链表~

有关**链表**的几种操作伪代码如下：

(链表有头指针)

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

### 10.3 指针和对象的实现

用数组来实现这个？没有兴趣，暂时不看...

## 第11章 散列表

### 11.1 直接寻址表

大眼一瞅，感觉说了半天就是在说普通的数组啊...

### 11.2 散列表


### 11.3 散列函数



### 11.4 开放寻址法



### 11.5 完全散列

















