---
layout: post
title: Selection Tree - Winner Tree (승자 트리)
description: >
   Selection Tree 중 Winner Tree (승자 트리)에 관한 이론 및 구현 방법
sitemap: false
hide_last_modified: true
---


# Selection Tree - Winner Tree (승자 트리)

---

<br>




## Selection Tree



<br>



>Selection Tree(선택 트리)란, 앞서 기술했던 Tree들처럼 Tree에 노드를 집어넣어 정렬시키는 방식이 아닌, ***노드들을 비교하여 하나씩 위로 올려 쌓아 나가는*** 일종의 **토너먼트 형식**이라고 할 수 있다. <br>
>
>말로는 이해하기 쉽지 않으니, 그림을 통해 이해하자.



<br>



> Selection Tree에는 Winner-Tree 와 Loser-Tree 가 있는데, 이번에는 Winner-Tree에 대해 알아보자.



<br>



![Winner-Tree](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAHrsM%2FbtqJii5jgKE%2FfKEfx32m1ZCIqIkDggTCak%2Fimg.png)



---

<br>



## Winner-Tree (승자 트리)



<br>



> Winner-Tree는 선택 트리의 한 종류로, 아래와 같은 특징을 가진다.



<br>



+ 부모 노드는 자식 노드보다 작은 값을 가지는 완전이진트리 이다.

+ 자매노드들 중 값이 더 작은 노드가 부모노드의 자리를 차지하는 토너먼트 형식을 취한다.

+ root 노드의 값이 모든 원소중 최소값이 된다.



---

<br>



## 구성



<br>



>먼저 **Run** 이라는 것에 대해 알아보자. <br>
>
>Run은 **가장 높은 level에 있는 노드들의 후보군**으로, 각 Run마다 여러개의 값이 이 있을 수 있다. <br>
>
>각 Run들은 최소값이 가장 앞에 위치하도록 정렬되어있으며, 각 Run에 담긴 값의 수는 상이할 수 있다.



<br>



1. 모든 Run의 맨 앞 원소를 각각의 leaf node에 담는다.

2. 두 자매노드 중 더 작은 값을 부모노드에 담는다. 

3. level을 하나씩 줄여가며 level 0에 도달할 때 까지(root node의 값이 정해질 때 까지)2의 과정을 반복한다. 

4. 첫 시행의 root node의 값이 모든 Run의 원소들 중 최소값이 된다.

5. root node를 pop시키고, 해당 값이 담겨있던 모든 노드에서 값을 지워버린다.

6. pop된 값이 담겨있던 Run에서 다음 값을 leaf node에 담는다.

8. 모든 Run의 원소가 tree에서 pop 될 때 까지 2 ~ 6의 과정을 반복한다.



<br>



>위 과정을 마치면 예를 들어 서울, 경기, 강원 등등 각 지역의 순위를 종합하여 전국 순위를 내야하는 상황과 같이 여러 집단을 종합해 결과를 도출해야 할 때 유용하게 사용할 수 있다.



---

<br>



## 장점



<br>



>위 과정을 제대로 따라왔다면 장점은 자연스럽게 알 수 있었을 것이다.  <br>
>
>**첫 시행에서는 많은 비교가 필요하지만 두번째 시행부터는 Tree의 level - 1 번의 반복만을 필요로 한다는 것**을 알 수 있다.  <br>
>
>이와 같이 시간복잡도의 측면에서 이점을 가진다. 



---

<br>



## 구현



<br>



>이를 실제로 코드로 구현하려면 은근히 생각이 꼬일 수 있는데, 아래 사실을 파악하고 시작하면 보다 쉽게 접근할 수 있을 것이다.



<br>



1. d 만큼의 깊이를 가지는 Tree에서의 최대 노드 수 : 2의 d제곱 - 1 개 

2. d + 1 level에서의 노드 개수 : 2의 d제곱 개

3. Winner-Tree를 두개로 나누어서 생각하자.

    1) Winner-Tree의 가장 하단 노드들을 저장할 배열

    2) 그 위의 Tree를 저장할 배열

    이처럼 Winner-Tree를 두 파트로 나누어서 생각하면 조금은 쉽게 구현할 수 있을 것이다. 

4. 3-2 배열을 구성할 때, Tree의 앞에서부터 채워나가도 상관 없지만, 뒤에서부터 채워나가는 것이 구현하기 용이할 것이다.



<br>



>이쯤에서 의문이 생겨야 한다. <br> <br>
>
>Run의 개수가 홀수이면 어떻게 처리해야 하나? <br>
>
>Run이 짝수개여도 6, 10과 같이 이상적인 Tree를 그릴 수 없는 상황에서는 어떻게 처리해야 하는가?



<br>



>이건 혼자 생각해보자. 충분이 해낼 수 있다.



<br>



https://m.blog.naver.com/gregchu/221450464344



---

<br>

