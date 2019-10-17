# Linked List
## 1. Single Linked List
#### Node Class
```C++
#include <iostream>
#include <string>

using namespace std;

class Node {
	friend class LinkedList;
private:
	int data;
	Node* Next;
public:
	Node() { data = NULL; Next = NULL; }
	Node(int _data) { data = _data; Next = NULL; }
	Node(int _data, Node *_node) { data = _data; Next = _node; }
};

class LinkedList {
private:
	Node *Head;
public:

	LinkedList() { Head = NULL; }
	~LinkedList() { delete_all(); }

	void insert_first(int data) {
		cout << "Insert " << data << endl;
		Head = new Node(data, Head);
	}

	void remove_first() {
		if (Head) {
			Node* tmp = Head;
			Head = Head->Next;
			cout << "Remove " << tmp->data << endl;
			delete tmp;
		}
		else {
			cout << "Linked List is empty" << endl;
		}
	}

	void delete_all() {
		while (Head != NULL) {
			Node* tmp = Head;
			Head = Head->Next;
			delete tmp;
		}
		cout << "* Delete all nodes" << endl;
	}
};

void main() {
	LinkedList stack;
	stack.insert_first(1);
	stack.insert_first(2);
	stack.insert_first(3);
	stack.insert_first(4);

	stack.remove_first();
	stack.remove_first();
}
```

#### Queue(TASK)
```C++
#include <iostream>
#include <string>

using namespace std;

class Node {
	friend class LinkedList;
private:
	int data;
	Node* Next;
public:
	Node() { data = NULL; Next = NULL; }
	Node(int _data) { data = _data; Next = NULL; }
	Node(int _data, Node *_node) { data = _data; Next = _node; }
};


class LinkedList {
private:
	Node *Head;
	Node *Tail;
public:

	LinkedList() { Head = NULL; Tail = NULL; }
	~LinkedList() { delete_all(); }

	void insert_last(int data) {
		cout << "Insert " << data << endl;
		/*
			Write down your own code
		*/
	}

	void remove_first() {
		/*
			Write down your own code
		*/
	}

	void delete_all() {
		while (Head != NULL) {
			Node* tmp = Head;
			Head = Head->Next;
			delete tmp;
		}
		cout << "* Delete all nodes" << endl;
	}
};

void main() {
	LinkedList stack;
	stack.insert_last(1);
	stack.insert_last(2);
	stack.insert_last(3);
	stack.insert_last(4);

	stack.remove_first();
	stack.remove_first();
	stack.remove_first();
	stack.remove_first();
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
