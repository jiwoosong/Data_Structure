# Linked List
## 1. Linked List
#### Basic Node Class + Linked List Class (with Append & Delete & Print member function)
```C++
#include <iostream>
#include <string>

using namespace std;

class Node {
public:
	int data;
	Node* Next;
};

class LinkedList {
public:
	Node *Head;
  
	LinkedList() {
		Head = NULL;
	}
  
	void append(int data) {
		Node * newNode = new Node();
		newNode->data = data;
		newNode->Next = NULL;

		Node *pNode = Head;
		if (pNode != NULL) {
			while (pNode->Next != NULL) {
				pNode = pNode->Next;
			}
			pNode->Next = newNode;
		}
		else {
			Head = newNode;
		}
	}

	void del(int data) {
		Node *pNode = Head;
		if (pNode == NULL) return;
		else if (pNode->Next == NULL) {
			if (data == pNode->data)
				delete pNode;
		}
		else {
			Node *nextNode;
			do {
				if (data == pNode->Next->data) {
					break;
				}
				pNode = pNode->Next;
			} while (pNode->Next != NULL);
			nextNode = pNode->Next;
			pNode->Next = pNode->Next->Next;

			delete nextNode;
		}
	}

	void printNode() {
		Node *current = Head;
		// Head 조차 비어있을 때
		if (current == NULL) {
			cout << "Empty Linked List" << endl;
		}
		// 노드가 하나만 존재할 경우
		else if (current->Next == NULL) {
			// Head 출력
			cout << current->data << " -> ";
			cout << "NULL" << endl;
		}
		else {
			// Head 출력
			cout << current->data << " -> ";
			current = current->Next;
			// Head->Next부터 Node 탐색
			while (current != NULL) {
				cout << current->data << " -> ";
				current = current->Next;
			}
			cout << "NULL" << endl;
		}
	}
};
void main() {
	LinkedList data;

	data.appendNode(1)
	data.appendNode(2)
	data.appendNode(3)
	data.appendNode(4)
	Fibonacci.printNode();
}
```

#### Basic Finbonacci algorithm
```C++
void main() {
	LinkedList Fibonacci;

	int F_current = 1;
	int F_next = 1;
	int num = 50;
	int tmp;

	cout << F_current << endl;
	for (int i = 0; i < num; i++) {
		cout <<F_next;
		tmp = F_next;
		F_next = F_next + F_current;
		F_current = tmp;
	}
	Fibonacci.printNode();
}
```

#### Linked List Fibonacci Code
Merge with above classes
```C++
void main() {
	LinkedList Fibonacci;

	int F_current = 1;
	int F_next = 1;
	int num = 50;
	int tmp;

	Fibonacci.append(F_current);
	for (int i = 0; i < num; i++) {
		Fibonacci.append(F_next);
		tmp = F_next;
		F_next = F_next + F_current;
		F_current = tmp;
	}
	Fibonacci.printNode();
}
```

## 2. Doubly Linked List
### Travel Node
```C++
#include <iostream>
#include <string>

using namespace std;

class Node {
public:
	string data;
	Node* Next;
	Node* Prev;
};

class DoublyLinkedList {
public:
	Node *Head;
	Node *Tail;

	DoublyLinkedList() {
		Head = NULL;
		Tail = NULL;
	}

	void append(string data) {
		Node * newNode = new Node();
		newNode->data = data;
		newNode->Next = NULL;
		newNode->Prev = NULL;

		if (Head != NULL) {
			Tail->Next = newNode;
			newNode->Prev = Tail;
			Tail = newNode;
		}else {
			Head = Tail = newNode;
		}
	}

	void del(string data) {
		Node *pNode = Head;
		if (pNode == NULL) return;
		else {
			Node *prevNode;
			Node *nextNode;
			
			do {
				if (data.compare(pNode->data) == 0) {
					break;
				}
				pNode = pNode->Next;
			} while (pNode != NULL);

			prevNode = pNode->Prev;
			nextNode = pNode->Next;

			// 삭제할 노드 이전의 노드가 없을 경우
			if (prevNode == NULL) {
				Head = nextNode;
			}else {
				prevNode->Next = nextNode;
			}

			//삭제하려는 노드의 다음 노드가 없는 경우
			if (nextNode == NULL) {
				Head = nextNode;
			}else {
				nextNode->Prev = prevNode;
			}

			delete pNode;
		}
	}

	void replace(string delete_data, string new_data) {
		/*
			Write down your own code
			
			요구사항 : 노드의 값 변경 금지, 노드를 교체방식 활용

		*/
	}

	void printNode() {
		Node *current = Head;
		// Head 조차 비어있을 때
		if (current == NULL) {
			cout << "Empty Linked List" << endl;
		}

		// 노드가 하나만 존재할 경우
		else if (current->Next == NULL) {
			// Head 출력
			cout << current->data << " -> ";
			cout << "NULL" << endl;
		}
		
		else {
			// Head 출력
			cout << current->data << " -> ";
			current = current->Next;
			// Head->Next부터 Node 탐색
			while (current != NULL) {
				cout << "<- " << current->data << " -> ";
				current = current->Next;
			}
			cout << "NULL" << endl;
		}
	}
};

void main() {
	DoublyLinkedList Travel;
	Travel.printNode();
	// 서울, 대전, 대구, 부산 추가
	Travel.append("Seoul");
	Travel.append("Daejeon");
	Travel.append("Daegu");
	Travel.append("Busan");
	Travel.printNode();

	// 제주도 독도 추가
	Travel.append("Jejudo");
	Travel.append("Dokdo");
	Travel.printNode();

	// 제주도 제거
	Travel.del("Jejudo");
	Travel.printNode();

	// 부산 -> 울릉도 대체
	Travel.replace("Busan", "Ulleungdo");
	Travel.printNode();

}
```
