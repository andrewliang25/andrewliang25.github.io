---
title: Binary-Tree-Traversal
tags:
---

{% asset_img binary-tree-example.png Binary Tree Example %}

Traversal means to go through all node on tree.

The most intuitive way in my mind is level-order way:\
Print all node on root level from left to right, and then its child level, and so on.\
Level order of example graph is `0 1 2 3 4 5 6 7 8 `.

But how about depth-first way?\
There are 3 actions when we move on a tree node:

<!-- more -->

+ V: Visiting, any operation on current node, i.e. print, assign...
+ L: Move to left child.
+ R: Move to right child.

For the order of these three actions with a constraint that `L` has to be front of `R`,\
we can get three permuations: `VLR`, `LVR`, `LRV`.\
Which is called pre-order, in-order, post-order, depend on where `V` is positioned.

Let us see code examples below:

## Binary Tree Data Structure
First, we need to define a tree node object.
A `TreeNode` contains a `int` value and two pointers reference to its two children.
```
// Go
type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}
```

## Level Order Traversal
Use queue to store nodes in same level.
```
// Go
// Iterative
func printTreeNodeLevelOrder(Root *TreeNode) {
	if Root == nil {
		return
	}
	Level := []*TreeNode{Root}

	for len(Level) > 0 { // while level is not empty
		NextLevel := []*TreeNode{}
		for _, Node := range Level { // Iterate through current level
			fmt.Printf("%v ", Node.Val) // Visiting
			// Push children into next level queue if existing
			if Node.Left != nil {
				NextLevel = append(NextLevel, Node.Left)
			}
			if Node.Right != nil {
				NextLevel = append(NextLevel, Node.Right)
			}
		}
		Level = NextLevel // Move on to next level
	}
}
```

## Preorder Traversal

```
// Go
// Recursive
func printTreeNodePreorder(Node *TreeNode) {
	if Node == nil {
		return
	}
	fmt.Printf("%v ", Node.Val)       // V
	printTreeNodePreorder(Node.Left)  // L
	printTreeNodePreorder(Node.Right) // R
}
```

## Inorder Traversal
```
// Go
// Recursive
func printTreeNodeInorder(Node *TreeNode) {
	if Node == nil {
		return
	}
	printTreeNodeInorder(Node.Left)  // L
	fmt.Printf("%v ", Node.Val)      // V
	printTreeNodeInorder(Node.Right) // R
}
```

## Postorder Traversal
```
// Go
// Recursive
func printTreeNodePostorder(Node *TreeNode) {
	if Node == nil {
		return
	}
	printTreeNodePostorder(Node.Left)  // L
	printTreeNodePostorder(Node.Right) // R
	fmt.Printf("%v ", Node.Val)        // V
}
```

## Result
Create a tree instance as example graph and call functions we have just implemented above.
```
// Go
func main() {
	var Root *TreeNode = &TreeNode{
		Val: 0,
	}
	Root.Left = &TreeNode{
		Val: 1,
	}
	Root.Right = &TreeNode{
		Val: 2,
	}
	Root.Left.Right = &TreeNode{
		Val: 3,
	}
	Root.Right.Left = &TreeNode{
		Val: 4,
	}
	Root.Right.Right = &TreeNode{
		Val: 5,
	}
	Root.Left.Right.Left = &TreeNode{
		Val: 6,
	}
	Root.Right.Right.Left = &TreeNode{
		Val: 7,
	}
	Root.Right.Right.Right = &TreeNode{
		Val: 8,
	}

	fmt.Println("Level Order")
	printTreeNodeLevelOrder(Root)

	fmt.Println("\nPreorder")
	printTreeNodePreorder(Root)

	fmt.Println("\nInorder")
	printTreeNodeInorder(Root)

	fmt.Println("\nPostorder")
	printTreeNodePostorder(Root)
}
```

And let us see the result with example graph:
{% asset_img binary-tree-example.png Binary Tree Example %}
```
Level Order
0 1 2 3 4 5 6 7 8 
Preorder
0 1 3 6 2 4 5 7 8 
Inorder
1 6 3 0 4 2 7 5 8 
Postorder
6 3 1 4 7 8 5 2 0 
Program exited.
```

> Reference
> https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/
> http://alrightchiu.github.io/SecondRound/binary-tree-traversalxun-fang.html
> https://shubo.io/iterative-binary-tree-traversal/
