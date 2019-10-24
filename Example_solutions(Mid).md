# 1. Review of C language
## Task 1
There is nothing attached because it is a task to run the given code.
## Task 2
There is nothing attached because it is a task to run the given code.
## Task 3
There is nothing attached because it is a task to run the given code.
## Task 4
```C++
#include <stdio.h>
struct student{
  const char *name;
  int student_num;
  double height;
  const char *bestfriend[3];
};
int main(void){
  struct student sewoong = {"sewoong", 2008035433, 191.9, {"SongJa", "MalJa", "Chamja"}}
  struct student *ptr;
  
  /*Answer*/
  ptr = &sewoong;
  ptr->name = "MSW";
  ptr->height = 180.3;  
  
  printf("student name : %s\n", ptr->name);
  printf("student num : %d\n", ptr->student_num);
  printf("student height : %.1f\n", ptr->height);
  printf("student friend1 : %d\n", ptr->bestfriend[0]);
  printf("student friend2 : %d\n", ptr->bestfriend[1]);
  printf("student friend3 : %d\n", ptr->bestfriend[2]);
}
```
# 2. Basic C++ 1 
## Task 1
```C++
#include <iostream>
#include <cstring>
#include <string>
using namespace std;

class Bird {
private:
	string name;
	int age;
public:
	void print_age(void);
	// declaration inside the class
	void print_name(void);
	void set_age(int);
	void set_name(string);
};
// declaration outside the class
/*Answer*/
void Bird::print_name(void) {
	cout << name << endl;
};
void Bird::set_age(int _age) {
	age = _age;
}
void Bird::set_name(string _name) {
	name = name + _name;
}
int main(void) {
	Bird a_bird;
  
  /*Answer(e.g.)*/
	a_bird.set_age(100);
	a_bird.set_name("Chamsae");
	a_bird.print_name();
}
```
## Task 2
```C++
#include <iostream>
#include <cstring>
using namespace std;

class Person {
private:
	string name;
	int age;
public:
	void print_age(void);
	void print_name(void);
	void set_age(int);
	void set_name(string);
};
void Person::print_age(void) {
	cout << age << endl;
}
void Person::print_name(void) {
	cout << name << endl;
}
void Person::set_age(int _age) {
	age = _age;
}
void Person::set_name(string _name) {
	name = _name;
}
class Student :public Person {
private:
	string school_name;
public:
	void input_school_name(string _school_name);
	void get_student_info(void);
};
void Student::input_school_name(string _school_name){
	school_name = _school_name;
}
void Student::get_student_info(void) {
	cout << "school is " << school_name << endl;
}
int main(void) {
	Student Younghee;

	string name = "Younghee";
	Younghee.set_name(name);
	Younghee.input_school_name("HANYANG");

	// didnt work? then try this
	Younghee.print_name();
	Younghee.get_student_info();

}
```
## TASK 3
```C++
#include <iostream>
#include <cstring>
using namespace std;

class Animal
{
public:
	virtual void say(void)
	{
		cout << "im animal" << endl;
	}
};
class Dog : public Animal
{
public:
	 void say(void)
	{
		cout << "bork" << endl;
	}
};

class Cat : public Animal
{
public:
	void say(void)
	{
		cout << "meow" << endl;
	}
};
int main(void)
{
	Dog* dog = new Dog();
	Cat* cat = new Cat();
	Animal* ani = new Animal();

	Animal* ani2 = new Dog();

	dog->say();
	cat->say();
	ani->say();

	ani2->say();
	

	return 0;
}
```
# 3. Basic C++ 1
## Task 1
```C++
#include <iostream>
#include <cstring>
using namespace std;

class Vector {
private:
	float x;
	float y;
public:
	Vector(float _x, float _y);  // constructor 
	~Vector();
	Vector operator-(Vector vec);
	Vector operator/(Vector vec);
	void print_coord(void);
};
Vector::Vector(float _x, float _y)
{
	cout << "constructor called" << endl;
	x = _x;
	y = _y;
}
Vector::~Vector()
{
	cout << "destructor called" << endl;
}
Vector Vector::operator-(Vector vec)
{
	return Vector(this->x - vec.x, this->y - vec.y);
}
Vector Vector::operator/(Vector vec)
{
	return Vector(this->x / vec.x, this->y / vec.y);
}
void Vector::print_coord()
{
	cout << "x:  " << x << endl << "y:  " << y << endl;
}


int main(void)
{
	Vector a(1., 1.);
	Vector b(1., 2.);

	Vector c = a - b;
	c.print_coord();;

	Vector d = a / b;
	d.print_coord();

	return 0;
}
```
# 4. Array & Dynamic Allocation
## Task1
```C++
#include <iostream>
using namespace std;
int main() {
	int i32cnt = 1;
	int ***array2D;
	array2D = new int **[3];
  
  /*Answer*/
	for (int i = 0; i < 3; i++) {
		array2D[i] = new int*[3];
		for (int j = 0; j < 3; j++) {
			array2D[i][j] = new int[3];
			for (int k = 0; k < 4; k++) {
				array2D[i][j][k] = i32cnt;
				i32cnt++;
			}
		}
	}
	for (int i = 0; i < 3; i++) {
		delete[] array2D[i];
	}
	delete[] array2D;
}
```
## Task2
```C++
#include <iostream>
#include <stdlib.h>
using namespace std;
void print_function(char **arr, int i) {
	cout << "Array [" << i << "] saved " << arr[i] << endl;
}
void main() {
	int n;
	char **name;
	char name_input[20];
	cout << "Number of people : ";
	cin >> n;
  /*Answer*/
	name = new char*[n];
	for (int i = 0; i < n; i++) {
    /*Answer*/
		cout << "name : ";
		cin >> name_input;
		name[i] = new char[strlen(name_input)];
		name[i] = name_input;
		print_function(name, i);
	}
}
```
# 5. Stack & Queue
## Task 1
```C++
```
## Task 2
```C++
#include<iostream>

using namespace std;

class Customer {
private:
	string name;
	bool data;
public:
	Customer(string _name = "None")
	{
		data = false;
		name = _name;
	}
	void set_data(bool _data)
	{
		data = _data;
	}
	void show_state() const
	{
		cout << name << "'s data is  " << data << endl;
	}
};

class Queue {
private:
	Customer* queue[5];
	int front, rear;
	int capacity = 5;
	bool is_empty() const;
public:
	Queue();
	~Queue();
	void push(Customer* data);
	void pop();
	void read_front() const;
	void read_rear() const;
	void check_queue() const;

};

Queue::Queue()
{
	front = -1;
	rear = -1;
}

Queue::~Queue() {
	delete[] queue;
}

void Queue::push(Customer* c)
{
	if ((rear - front) == -1 || ((rear - front) == capacity))
		cout << "queue is full" << endl;
	else
	{
		queue[++rear] = c;
	}
}

bool Queue::is_empty() const {
	return rear == front;
}

void Queue::pop()
{
	if (is_empty())
		cout << "Queue is empty" << endl;
	else {
		queue[++front]->set_data(true);
	}
}

void Queue::read_front() const {
	cout << "Front is " << front << endl;
}

void Queue::read_rear() const {
	cout << "Rear is " << rear << endl;
}

void Queue::check_queue() const {
	if (front <= rear)
	{
		for (int i = front + 1; i < rear + 1; i++)
			queue[i]->show_state();
		cout << endl;
		cout << "Total number of data is " << (rear - front);


	}
	else {
		for (int i = front + 1; i < capacity; i++)
			queue[i]->show_state();
		for (int i = 0; i < rear + 1; i++)
			queue[i]->show_state();
		cout << endl;
		cout << "Total number of data is " << (10 + rear - front);
	}
	cout << endl;
	read_front();
	read_rear();
	cout << endl;
}

int main() {
	Customer c1("jake"), c2("grace"), c3("dave"), c4("peter"), c5("youjean");
	Queue q;

	q.push(&c1);
	q.push(&c2);
	q.push(&c3);
	q.push(&c4);
	q.push(&c5);

	q.check_queue();
	q.pop();
	q.check_queue();
	q.pop();
	q.check_queue();
	q.pop();
	q.check_queue();
	q.pop();
	q.check_queue();
	q.pop();

	c1.show_state();
	c2.show_state();
	c3.show_state();
	c4.show_state();
	c5.show_state();

	q.pop();

	return 0;
}
```
# 6. Linked List
## Task 1
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
		if (Tail == NULL) {
			Tail = new Node(data);
			Head = Tail;
		}
		else {
			Tail->Next = new Node(data);
			Tail = Tail->Next;
		}
	}
	void remove_first() {
		if (Tail) {
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
## Task 2
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
		}
		else {
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
			}
			else {
				prevNode->Next = nextNode;
			}
			//삭제하려는 노드의 다음 노드가 없는 경우
			if (nextNode == NULL) {
				Head = nextNode;
			}
			else {
				nextNode->Prev = prevNode;
			}
			delete pNode;
		}
	}
	void replace(string delete_data, string new_data) {
    /*Answer*/
		Node *pNode = Head;
		if (pNode == NULL) return;
		else {
			Node *prevNode;
			Node *nextNode;
			do {
				if (delete_data.compare(pNode->data) == 0) {
					break;
				}
				pNode = pNode->Next;
			} while (pNode != NULL);
			prevNode = pNode->Prev;
			nextNode = pNode->Next;
			// 대체할 노드 생성
			Node * newNode = new Node();
			newNode->data = new_data;
			newNode->Next = nextNode;
			newNode->Prev = prevNode;
			// 삭제할 노드 이전의 노드가 없을 경우
			if (prevNode == NULL) {
				Head = nextNode;
			}
			else {
				prevNode->Next = newNode;
			}
			//삭제하려는 노드의 다음 노드가 없는 경우
			if (nextNode == NULL) {
				Head = nextNode;
			}
			else {
				nextNode->Prev = newNode;
			}
			delete pNode;
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
