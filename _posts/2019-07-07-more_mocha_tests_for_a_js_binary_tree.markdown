---
layout: post
title:      "More Mocha Tests For a JS Binary Tree"
date:       2019-07-07 17:14:48 -0400
permalink:  more_mocha_tests_for_a_js_binary_tree
---

Continuing from my last post, I have kept adding methods to my binary tree class and tests to accompany them. I added an inorder traversal and a search function. First, the inorder method: 
```
    inorder(node){
        function inorderHelper(node){
            if (node){
                inorderHelper(node.left) 
                treeArr.push(node.id)
                inorderHelper(node.right) 
            }
        }
        const treeArr = []
        inorderHelper(node)
        return treeArr
    }
```
I decided to keep the helper function in the scope of the parent function so that I could push to and return a single array instead of console.log-ing all of the node ids. The helper function is a straightforward recursive function. Find the left-most node, push that node to the array, and then move to the parent and ultimately right-ward. I chose in order as it would produce a sorted array for this binary tree. The test for this method was:
```
    let head = new nodeClass(50)
    let tree = new binaryTreeClass(head)       
    let node70 = new nodeClass(70)
    let node30 = new nodeClass(30)
    let node10 = new nodeClass(10)
		
    it('A tree can be traversed inorder', function(){
        tree.addNode(node70)
        tree.addNode(node30)
        tree.addNode(node10)
        expect(tree.inorder(head)).to.eql([10,30,50,70]) 
    })
```

I defined the nodes and the tree in the main Binary tree test closure so that they could be used repeatedly. I attach them in the individual tests to keep the tests singular. I initially tried to use 
```
assert.equal(tree.inorder(head), [10,30,50,70])
```
but this failed when they were the same. I'm not completely sure why this is but my understanding is that it is checking if they are the same object, which they are not. 

For the search function, I had:
```
    search(nodeId, node){
        if (node){
            if (nodeId === node.id){
                return node.id;
            } else if (nodeId > node.id){
                if (node.right){
                    return this.search(nodeId, node.right)
                } else {
                    return "Id is not in tree."
                }
            } else {
                if (node.left){
                    return this.search(nodeId, node.left)
                } else {
                    return "Id is not in tree."
                }
            }
        } else {
            return 'Id is not in tree.'
        }
    }
```
This method compares the id to the head, then moves to the left or right child accordingly. If the id exists in the tree, return that id. If the id is smaller or larger than a node and the child that we try to visit does not exist, that value does not exist in the tree. To test, this 
```
   it('A tree can be searched', function(){
        
        tree.addNode(node70)
        tree.addNode(node30)
        tree.addNode(node10)
        assert.equal(tree.search(30, head), 30)
        assert.equal(tree.search(40, head), 'Id is not in tree.')
    })
```
