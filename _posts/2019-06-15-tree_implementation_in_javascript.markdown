---
layout: post
title:      "Tree Implementation in JavaScript"
date:       2019-06-15 17:45:01 +0000
permalink:  tree_implementation_in_javascript
---


I was recently given an open ended, domain based coding challenge. Without being too specific, it was a situation where a tree data structure would fit perfectly. The problem for me was that I had not implemented a tree structure in a very long time. Instead of trying to figure out how to implement it, I tried to use a basic array structure that ultimately did not lead to anything. The time pressure got to. I decided that instead of trying to figure out a tree structure with a chance of not getting any tests to pass I would instead ensure that I got a few of them to. Looking back this was not a good decision.

After the challenge ended, I immediately went to VS code to remind myself how to set up a tree and traverse it. To apply it to a real world scenario I used the domain of emplyees and managers. First, I defined a node class.
```
class Node {
    constructor(nodeId, name, parentId){
        this.nodeId = nodeId
        this.name = name
        this.parentId = parentId 
        this.parent = null
        this.children = []
    }

}
```
This node just stores the basic information for one unit, which in this case is just a person. A tree is just a collection of nodes that are connected as parents and children. To put that basic idea in action, I created a tree class with a contructor and an add node method

```
class Tree {

    constructor() {
        this.root = null
    }


    addNode(nodeId, name, parentId){
        let node = new Node(nodeId, name, parentId)

        if (!this.root){
            this.root = node
        } else {
            let foundNode = this.search(this.root, parentId)
            node.parent = foundNode 
            foundNode.children.push(node)
        }
		}
	}
```

The addNode method instantiates a new node and either establishes it as the root or adds it as a child to a node. This would work to create the tree, but its not very useful if it can't be traversed. 
```
    traverse(node, cb){
		    cb.call(node)
        if (node.children){
            for (let i=0; i<node.children.length; i++){
                this.traverse(node.children[i], cb)
            }
        }
    }
```

This function recursively checks all nodes in a preorder traversal. It includes a callback function that can be called on a node. This will be used in the print function. 
```
    print(){
        function printCB(depth) {
            console.log(`${this.name} [${this.nodeId}]`)
        }
        this.traverse(this.root, printCB)
    }
```
I used a normal function for the callback instead of an arrow function so that I could bind a node as this in the traverse method. While I could have simply used console.log in the traverse method, I wanted to keep it general. Partially since this was just practice but also to potentially add more complex callbacks in the future. Ideas for these could be printing nodes differently based on their depth or altering the data in all nodes at once. 

