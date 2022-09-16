---
title: Binary-Tree-Traversal
tags:
---

<!-- more -->

## Binary Tree Data Structure
```
// Go
type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}
```

## Level Order Traversal
```
// Go
func printTreeNodeLevelOrder(Root *TreeNode) {
	if Root == nil {
		return
	}
	Level := []*TreeNode{Root}
	for len(Level) > 0 {
		NextLevel := []*TreeNode{}
		for _, Node := range Level {
			fmt.Printf("%v ", Node.Val)
			if Node.Left != nil {
				NextLevel = append(NextLevel, Node.Left)
			}
			if Node.Right != nil {
				NextLevel = append(NextLevel, Node.Right)
			}
		}
		Level = NextLevel
	}
}
```

## Preorder Traversal

```
// Go
func printTreeNodePreorder(Node *TreeNode) {
	if Node == nil {
		return
	}
	fmt.Printf("%v ", Node.Val)
	printTreeNodePreorder(Node.Left)
	printTreeNodePreorder(Node.Right)
}
```

## Inorder Traversal
```
// Go
func printTreeNodeInorder(Node *TreeNode) {
	if Node == nil {
		return
	}
	printTreeNodeInorder(Node.Left)
	fmt.Printf("%v ", Node.Val)
	printTreeNodeInorder(Node.Right)
}
```

## Postorder Traversal
```
// Go
func printTreeNodePostorder(Node *TreeNode) {
	if Node == nil {
		return
	}
	printTreeNodePostorder(Node.Left)
	printTreeNodePostorder(Node.Right)
	fmt.Printf("%v ", Node.Val)
}
```

> Reference
> https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/
> http://alrightchiu.github.io/SecondRound/binary-tree-traversalxun-fang.html
> https://shubo.io/iterative-binary-tree-traversal/