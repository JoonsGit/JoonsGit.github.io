---
layout: post
title: Binary Tree_보충
description: >
   Binary Tree(이진트리)에 관한 보충 학습 
sitemap: false
hide_last_modified: true
---


# Binary Tree (이진트리) - 보충



---

<br>


**Tree에 대해 부족했던 부분들을 보충해보자.**



<br>



---

<br>



## Tree의 조건



> 1. 회로 (circuit)가 존재하면 안된다.
> 1. 특정 노드로 가는 path가 유일해야 한다.
> 1. 연결되지 않은 노드가 존재하면 안된다.



---

<br>



## Binary Tree?

<br>

이진트리란, **자식 노드가 최대 두 개인 노드들로 구성된 트리**를 뜻한다.



<br>



> 종류 : **정이진트리(full binary tree), 완전이진트리(complete binary tree), 균형이진트리(balanced binary tree)** 등등



<br>



### 정이진트리/포화이진트리(full binary tree)



<br>



![정이진트리](https://i.imgur.com/edCd7lU.png)



<br>



> 잎새노드를 제외한 모든 노드가 두개의 자식 노드를 가지고 있는 이진트리.   



<br>



### 완전이진트리(complete binary tree)



<br>



![완전이진트리](https://i.imgur.com/mXssEqj.png)



<br>



> 마지막 레벨을 제외한 모든 레벨에서 노드들이 꽉 채워진 이진트리.
>
> 마지막 레벨은 왼쪽부터 빈틈 없이 채워져 있어야 한다.



***정이진트리와 완전이진트리는 1차원 배열로도 표현이 가능하다.***



<br>



![배열표현](https://i.imgur.com/3sUWVY2.png)



<br>



### 균형이진트리(balanced binary tree)



<br>



![균형이진트리](https://i.imgur.com/hPuxfES.png)



<br>



> 모든 잎새노드의 깊이 차이가 많아야 1인 이진트리.
>
> 균형이진트리는 예측 가능한 깊이(predictable depth)를 가지며, 노드가 n개인 균형이진트리의 깊이는 ***log n*** 을 내림한 값이 된다.



---

<br>



## Tree Traversal (트리 순회)



<br>



> 말 그대로 트리의 각 노드를 체계적인 방법으로 방문하는 과정을 말한다.
>
> Inorder, preoder, postoder, levelorder 총 네가지 방법이 있는데, levelorder를 제외한 방법들은 이전에 기술했으니 생략한다.



<br>



### Level-order Traversal



<br>



> 레벨을 위에서부터 하나씩 탐색하는 방법.



<br>



![레벨오더](https://github.com/ChanhuiSeok/chanhuiseok.github.io/blob/master/assets/img/sample/ds_2.png?raw=true)



<br>



> 예를 들어, 위의 트리를 levelorder의 방법으로 탐색하면 A -> B -> C -> D -> E -> F -> G 이 순서로 탐색하게 된다.



<br>



### leverorder의 구현



<br>



> level-order는 **queue**로 구현하는 것이 편하다.
>
> root 노드부터 시작하여 enqeue시킨다. 
>
> FIFO 방식에 의거하여 노드를 하나씩 deque 하는 과정에서 deque된 노드의 left child node, right child node 를 차례로 enque 시킨다.
>
> 노드들은 deque 되는 동시에 출력된다. 



<br>



위와 같은 방식으로 간단하게 이진트리를 탐색할 수도 있다. 



<br>



---

