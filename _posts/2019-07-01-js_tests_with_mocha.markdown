---
layout: post
title:      "JS tests with Mocha"
date:       2019-07-01 18:52:48 +0000
permalink:  js_tests_with_mocha
---


The curriculum at Flatiron was centered around test-driven development. They used RSpec for Ruby and Mocha for JavaScript. Although there were occasional issues the tests passed correctly almost all of the time. I became familiar with these frameworks by using them but never actually wrote any tests myself. After seeing that experience in test-driven development was recommended for a lot of job postings, I decided that it was time to actually write some tests. 

Since most of my coding these days is JavaScript I decided to learn Mocha. After creating a directory, intializing a package.json file, and npm installing Mocha I also installed Chai. From what I understand, Chai is an assertion library that is more robust than the default assertion library. I hope to understand this more as I continue writing tests. 

I followed along a Youtube tutorial for the basic infrastructure of Mocha, but I'll share what I worked on after.

From the root of the project I made a data_structures folder that contained node.js and binaryTree.js files:

From node.js :
```
class Node {
    constructor(id, name){
        this.id = id;
        this.numDuplicated = 0;
        this.left = null;
        this.right = null; 
    }
}

module.exports = Node
```
binaryTree.js: 
```
class BinaryTree {
    
    constructor(head){
        this.head = head;
    }    

    addNode(newNode){
        let node = this.head;
        while(node){
            if (newNode.id > node.id){
                if (node.right){
                    node = node.right;
                } else {
                    node.right = newNode;
                    return 
                }
            } else if(newNode.id < node.id){
                if (node.left){
                    node = node.left;
                } else {
                    node.left = newNode; 
                    return 
                }
            } else {
                node.numDuplicates++;
                return; 
            }
        }
    }

}

module.exports = BinaryTree
```

Then, from the root again I made a test folder with data_structuresTest.js. Here, I first added the necessary imports:
```
const assert = require('chai').assert;
const nodeClass = require('../data_structures/node.js')
const binaryTreeClass = require('../data_structures/binaryTree')
```
Since the I default exported the classes from their files I can directly refer to them with require. Now to test the Node class. This just had one test to see if it could be instantiated. 
```
describe("Node", function(){
    it ('A node can be instantiated', function(){
        let myNode = new nodeClass(1);
        assert.equal(myNode.id, 1)
        assert.equal(myNode.numDuplicated, 0)
    })
})
```
Once that passed, I went on to test the binary tree class. This class only has a method for inserting a node, so the tests would insert a node and then manually test the connections to make sure it is correctly placed.
```
describe("BinaryTree", function(){

    let head = new nodeClass(50)
    let tree = new binaryTreeClass(head)
    
    it('A tree can be instantiated', function(){
        assert.equal(tree.head, head)
    })

    it('A node can be added', function(){
        let node70 = new nodeClass(70)
        let node30 = new nodeClass(30)
        tree.addNode(node70)
        tree.addNode(node30)
        assert.equal(head.right, node70)
        assert.equal(head.left, node30)
    })
})
```
I was trying to use a beforeEach hook to declare the head and tree as I did at the top of the block. My hope was to declare those two variables each time a test was about to be run in the block to ensure that each test ran independently. From what I understand that is something that I should be able to do but could not figure it out. I hope to figure that out.
