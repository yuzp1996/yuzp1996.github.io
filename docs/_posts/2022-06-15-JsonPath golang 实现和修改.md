## JsonPath 解析和使用
### 背景

见识下工业级 jsonpath 实现      吃一下 jsonpath 的苦

client-go 中的 jsonpath 实现，其中包含 Parser 和 Node 新的结构体

parse 先把body给变成一个一个的不同类型的 node

然后后面是根据这些node来处理的data   findAllResults  （这里返回的是 reflect 所以可以直接进行使用了   我们目前是在这里直接处理的 reflect 的值  保证好使）

然后根据传入的 data 有可能是struct 通过 reflect 处理  然后 Print 的时候 找到这些值 然后再输出出来


而且目前发现 还可以使用自带的 debug 功能来做这些事情 感觉很棒 很好

把这个吃透了 将会真正的提升一个 level

递归 指针 反射 debug

目标 完善好这个文章 将里面涉及到的面全部搞定
```
type JSONPath struct {
	name       string
	parser     *Parser
	beginRange int
	inRange    int
	endRange   int

	lastEndNode *Node

	allowMissingKeys bool
	outputJSON       bool
}


type Parser struct {
	Name  string
	Root  *ListNode
	input string
	pos   int
	start int
	width int
}

// ListNode holds a sequence of nodes.
type ListNode struct {
	NodeType
	Nodes []Node // The element nodes in lexical order.
}

type Node interface {
	Type() NodeType
	String() string
}


```


### 如何使用

### 如何修改

### 现状

### 你也试试？
