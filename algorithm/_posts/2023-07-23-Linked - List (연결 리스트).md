---
layout: post
title: Linked-List (연결 리스트)
description: >
 Linked-list에 관한 이론적인 설명
sitemap: false
hide_last_modified: true
---

# Linked List (연결 리스트)

***
<br>

**자료구조**는 **데이터의 표현 및 저장 방법**을 의미하며, **특정한 형태로 저장된 데이터를 처리하는 과정 및 방법**을 **알고리즘**이라 칭한다. 때문에 본격적으로 알고리즘 공부를 시작하기 전에 자료구조에 대한 이해도를 높일 수 있다면 알고리즘 공부시에 많은 이점을 취할 수 있을 것이니, 자료구조를 하나하나 천천히 살펴보도록 하자.

<br>

***

<br>

## Linked List ?

> Linked List란 어떠한 자료의 구조를 일컫는 말일까? 우리는 그 해답을 비교적 손쉽게 알아낼 수 있다. 구조의 이름은 그 본연의 형태에서 아이디어를 얻어 지어지기 마련인데, 그런 의미에서 Linked List는, 말 그대로 **여러개의 객체들이 List의 형태로 존재하는데, 각각의 객체들이 한 방향 혹은 여러 방향으로 연결된 형태의 자료구조**를 의미한다.
<br>

> Linked List는 기본적으로 여러개의 **Node(일종의 객체)** 가 연결된 구조인데, 각 Node에는 고유의 데이터와 다음 객체를 가리키는**주소(포인터)** 를 가지고 있다. 또한 대부분의 상황에서 Node의 데이터 변수는 **private** 혹은 **protected** 의 형태로 저장되어 있기 때문에, 새로운 데이터를 추가하거나, 기존의 데이터를 수정하는 경우, 가리키는 다음 Node의 주소를 가리키는 포인터 변경 등의 기능을 수행하는 함수들 역시 기본적으로 지니고 있어야 프로그램이 정상적으로 동작 할 수 있게 된다.
<br>

> 연결 리스트는 크게 **Singly-Linked List(단방향 연결 리스트), Doubly-Linked List(이중 연결 리스트), Multi-Linked List(다중 연결리스트)** 로 구분지을 수 있는데, 아래에서 코드를 기반하여 하나씩 살펴보자.  

<br>

***
<br>

### Singly- Linked List (단방향 연결 리스트)
<br>

![연결 리스트](https://velog.velcdn.com/images/kon6443/post/7b18a6f4-3c6c-4b48-8b7a-5fbe8757b773/image.png)
<br>


> 위 그림에서 SLL의 구조에 대해 이해해보자.
<br>

+ 첫번째 Node는 **head** 라고 불린다.<br>
+ list의마지막 Node는 **Tail** 이라 불린다. <br>
+ 리스트가 비어있다면, head는 **Null**을 가리킨다.<br>
+ Data 변수의 data type은 원하는 형태로 저장할 수 있다.<br>
+ 각각의 Node들은 기본적으로, 데이터를 저장할 **Data 변수**와 다음 Node를 가리키는 **Pointer 변수**를 가지고 있다.<br><br>

> 아래는 CPP로 링스드 리스트를 구현한 간단한 예제이다.
<br>

```cpp
// C++ program for the above approach
#include <iostream>
using namespace std;

// Node class to represent
// a node of the linked list.
class Node {
public:
	int data;
	Node* next;

	// Default constructor
	Node()
	{
		data = 0;
		next = NULL;
	}

	// Parameterised Constructor
	Node(int data)
	{
		this->data = data;
		this->next = NULL;
	}
};

// Linked list class to
// implement a linked list.
class Linkedlist {
	Node* head;

public:
	// Default constructor
	Linkedlist() { head = NULL; }

	// Function to insert a
	// node at the end of the
	// linked list.
	void insertNode(int);

	// Function to print the
	// linked list.
	void printList();

	// Function to delete the
	// node at given position
	void deleteNode(int);
};

// Function to delete the
// node at given position
void Linkedlist::deleteNode(int nodeOffset)
{
	Node *temp1 = head, *temp2 = NULL;
	int ListLen = 0;

	if (head == NULL) {
		cout << "List empty." << endl;
		return;
	}

	// Find length of the linked-list.
	while (temp1 != NULL) {
		temp1 = temp1->next;
		ListLen++;
	}

	// Check if the position to be
	// deleted is greater than the length
	// of the linked list.
	if (ListLen < nodeOffset) {
		cout << "Index out of range"
			<< endl;
		return;
	}

	// Declare temp1
	temp1 = head;

	// Deleting the head.
	if (nodeOffset == 1) {

		// Update head
		head = head->next;
		delete temp1;
		return;
	}

	// Traverse the list to
	// find the node to be deleted.
	while (nodeOffset-- > 1) {

		// Update temp2
		temp2 = temp1;

		// Update temp1
		temp1 = temp1->next;
	}

	// Change the next pointer
	// of the previous node.
	temp2->next = temp1->next;

	// Delete the node
	delete temp1;
}

// Function to insert a new node.
void Linkedlist::insertNode(int data)
{
	// Create the new Node.
	Node* newNode = new Node(data);

	// Assign to head
	if (head == NULL) {
		head = newNode;
		return;
	}

	// Traverse till end of list
	Node* temp = head;
	while (temp->next != NULL) {

		// Update temp
		temp = temp->next;
	}

	// Insert at the last.
	temp->next = newNode;
}

// Function to print the
// nodes of the linked list.
void Linkedlist::printList()
{
	Node* temp = head;

	// Check for empty list.
	if (head == NULL) {
		cout << "List empty" << endl;
		return;
	}

	// Traverse the list.
	while (temp != NULL) {
		cout << temp->data << " ";
		temp = temp->next;
	}
}

// Driver Code
int main()
{
	Linkedlist list;

	// Inserting nodes
	list.insertNode(1);
	list.insertNode(2);
	list.insertNode(3);
	list.insertNode(4);

	cout << "Elements of the list are: ";

	// Print the list
	list.printList();
	cout << endl;

	// Delete node at position 2.
	list.deleteNode(2);

	cout << "Elements of the list are: ";
	list.printList();
	cout << endl;
	return 0;
}

```
<br>

***
<br>

### Doubly- Linked List (DLL / 이중 연결 리스트)
<br>

![연결 리스트](https://velog.velcdn.com/images/kon6443/post/8ec95fb8-f679-49d4-9b24-5cbbef3d7c3d/image.png)
<br>


> 실무적으로는 더블 링크스 리스트 라는 말로 더 자주 불리는 DLL의 구조에 대해, 위의 그림을 통해 이해해보자.
<br>

+ 첫번째 Node는 **head** 라고 불린다.<br>
+ 마지막 Node는 **Tail** 이라 불린다. <br>
+ 리스트가 비어있다면, head는 **Null**을 가리킨다.<br>
+ Data 변수의 data type은 원하는 형태로 저장할 수 있다.<br>
+ SLL과는 다르게 DLL은 현재 Node의 *다음 Node를 가리키는* **Next Pointer** 이외에 *이전 Node를 가리키는* **Prev Pointer** 또한 가지고있어야 한다.<br><br>

> 이외에도 **Multi-Linked List(MLL / 다중 연결 리스트), Circular-Linked list(CLL / 원령 연결 리스트)** 가 있는데, 이 둘도 기본 컨셉은 위의 두 Linked List 형태와 같음으로 간단하게 특징 정도만 알아보자.

<br>

---
<br>

### Mulit-Linked list(MLL / 다중 연결 리스트)
<br>

> 사실 이전에 설명한 DLL 또한 MLL의 한 가지이긴 하다. 다음 Node만을 바라볼 수 밖에 없는 SLL에 비해, MLL은 Next Node 이외의 Node를 바라볼 수 있는 구조를 의미하기 때문에 그렇다 할 수 있는 것이다.<br>

**그렇다면 SLL에 비해 MLL의 장단점은 무엇이 있을까?**<br>

> 가장 먼저 떠오르는 장점은 역시 탐색 속도에 있다. 단발적인 탐색이 아닌, 연속적으로 탐색이 이루어져야하는 경우 시간이 크게 단축된다는 효과가 있다. 하지만 Next Pointer만을 가진 SLL에 비해 두배 이상의 Pointer 공간이 사용되어야 한다는 단점 또한 존재한다.<br>

**DLL 이상의 MLL은 어떻게 구현할 수 있을까**<br>

> 예를 들어 Next 와 Prev Pointer 가 아닌, 두개의 Next Pointer를 가져야 하는 상황은 어떻게 구현해야 할까? 당장 떠오르는 방법으로는, pointer 변수를 vector의 동적 할당을 통해 하나의 Node에 포인터를 다중으로 사용하는 방법이 있겠다.<br>

<br>

---
<br>

### Circular-Linked list (CLL / 원형 연결 리스트)
<br>

> CLL은 생각보다 간단하다. 단순하게 list가 원형으로 연결된 구조라고 생각하면 되는데, Tail Node의 Next Pointer가 Head Node의 주소값을 가리키도록 설정하면 간단히 CLL을 완성할 수 있다.<br>

> 장점으로는 모든 Node의 탐색을 끝마치면 다시 탐색 초기 Node로 돌아올 수 있다는 점, 비교적 단순한 구조를 가질 수 있다는 것 정도가 있겠다.<br>

<br>

---
<br>
