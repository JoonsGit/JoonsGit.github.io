---
layout: post
title: Stack & Queue (스택 & 큐)
description: > 
  Stack(스택)과 Queue(큐)에 관한 기본적인 이론
sitemap: false
hide_last_modified: true
---


# Stack & Queue (스택 & 큐)

---

<br>


#### Stack 과 Queue는 비슷하지만 다른 자료구조로, 한번에 비교하여 확인하는 것이 간편하다 생각되어 함께 기술한다.<br>



---

<br>


## Stack (스택)

<br>



> Stack(스택)은 실생활에서도 흔히 포착할 수 있는 자료구조 중 하나로, 연결 리스트인데, **뒤로 넣고 뒤로만 뺄 수 있는 구조**라고 생각하면 편리하다. 예를 들자면, 이사를 하게 되어 이삿짐을 옮기는 와중에 쌓여있는 박스들을 옮기려면 어떻게 하는가? 일반적으로는 가장 위에 있는 박스부터 하나씩 옮길 것 이다. 가장위에 있는 박스는 쌓여있는 박스들 중 가장 나중에 쌓인 박스라고도 할 수 있는데, 이와 같이 ***가장 나중에 추가된 데이터부터 리스트에서 뺄 수 있는 구조***를 Stack이라고 한다<br>



> 위와 같은 구조를 흔히 **LIFO**(Last-In-First-out / 후입선출) 구조라고 하는데, 말 그대로 후위에 들어온 데이터 부터 빠져나갈 수 있다는 의미이다. 이해가 잘 되지않는다면 아래 그림을 통해 살펴보자.<br>

<br>



![stack](https://blog.kakaocdn.net/dn/by1qnT/btqBE1v1UlX/zbnXdYnGAXhMYbcDCca6WK/img.png)

<br><br>



> 위 그림에서 알 수 있듯이 stack에서는 push와 pop이라는 명령을 수행하는데, 자주 사용되는 명령어 몇가지만 알아보자.<br>

<br>



+ push(a) : a 를 스택 맨 위에 삽입<br>

+ pop() : 스택 맨 위에 있는 항목을 삭제<br>

+ empty() : 스택이 비어있다면 true를, 비어있지 않다면 false를 반환<br>

+ size() : 스택에 들어있는 원소의 개수를 반환<br>

+ top() : 스택의 맨 위에 있는 항목을 반환<br>

<br>



> 이와 같은 명령들을 실행하는 와중에 여러가지 에러가 발생하곤 하는데, 혹시 **stack overflow**라는 말을 들어본 적이 있는가? 유명한 해외 프로그래밍 질의응답 커뮤니티의 이름으로도 알려진 이 용어는 주어진 ***stack의 메모리를 초과하여 데이터를 삽입하려고 할 때 발생하는 에러***로, 재귀함수나 여러 함수가 중첩되어 호출되는 경우에 빈번히 발생한다. 이와 반대로 **stack underflow**라는 에러도 익히 발생하는데, ***stack이 empty한 상태에서 데이터를 추출하려고 할 때 발생하는 에러***라고 생각하면 된다.<br>



#### 시간 복잡도의 측면에서 생각하면 어떠할까?<br>



> 새로운 값을 push 하는데 O(1), 값을 빼는데 O(1), top data를 확인하는데 O(1)이다.

<br>



---

<br>


## Queue (큐)

<br>



> **Queue(큐)** 또한 Stack과 유사한 자료구조인데, stack과 구별되는 점은 데이터의 삽입 및 추출 방식에서 찾아볼 수 있다. Queue는 ***가장 먼저 삽입된 데이터가 가장 먼저 추출되는 구조***로, **FIFO**(First-In-First_Out / 선입선출) 구조를 띄고 있다. 아래 그림을 통해 쉽게 이해해보자.<br>

<br>



![queue](https://images.velog.io/images/oeueoo/post/e4c05fdb-b2a0-4289-b5b2-5c3737543c0d/KakaoTalk_Photo_2021-08-17-19-09-51.jpeg)

<br><br>



> 위의 그림에서 왼쪽의 그림은 위에서 기술한 LIFO 구조를, 오른쪽은 FIFO 구조를 설명한다. enqueue, dequeue가 뭔지 궁금할텐데, 아래에서 자주 사용되는 명령들을 살펴보자.<br>

<br>



+ enqueue(a) : a 항목을 큐의 가장 뒤에 삽입<br>

+ dequeue() : 큐의 가장 앞에 있는 데이터를추출<br>

+ front() : 큐의 맨 앞에 있는 데이터를 리턴<br>

+ rear() : 큐의 맨 뒤에 있는 데이터를 리턴<br>

+ empty() : 큐가 비어있다면 true, 비어있지 않다면 false를 리턴<br>

+ size() : 큐의 사이즈를리턴<br>

<br>



> queue의 **시간 복잡도는 stack과 동일**하다.<br>



> 주로 stack이나 queue는 데이터가 추가되거나 추출 될 때 마다 사이즈가 바뀌기 때문에 주로 Linked-List로 구현하는데, 이렇게 큐를 구현하게 되면 **순환 큐**나 **우선순위 큐**와 같이 특수한 형태의 큐도 구현할 수 있게 된다.<br>



### 순환 큐

<br>



> 순환 큐는 큐의 **front와 rear가 연결되어 있는 구조의 큐**로, 주로 메모리를 간편하게 관리하기 위해 사용한다. 예를 들면 1, 2, 3, 4, 5 라는 5개의 데이터가 있을 때, 기본 형태의 큐 라면 1 ~ 5 까지 탐색하면 끝내야 하지만, 순환 큐의 경우에는 rear인 5를 탐색한 후에 front인 1로 다시 돌아오는 구조로, ***rear의 next를 front로 설정함으로써 구현할수 있다.*** <br>

<br>



### 우선순위 큐 

<br>



> 우선순위 큐는 기본 형태의 큐와 달리 enqueue()를 실행하여 데이터가 삽입될 때 무조건적으로 가장 뒤에 삽입하는 것이 아닌, **프로그래머가 정해놓은 우선순위 기준에 따라 알맞은 위치에 데이터를 삽입하는 구조**이다. 

<br>



---

<br>

