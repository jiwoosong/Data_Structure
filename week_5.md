# Stack & Queue
## 1.Stack 
### - Example 2 code 
```c++
#include <iostream>

using namespace std;

class Stack {
private:
	int N;								// 스텍 size 변수
	int* stack;							// 스텍 데이터
	int top;							// top 위치
public:
	Stack(int size);					// 스텍 데이터 공간 할당
	~Stack();							// 스텍 데이터 공간 제거
	void push(int value);				// 데이터 넣기
	void pop();							// 데이터 빼기
	int read_top();						// top 값 확인
	void check_stack();					// 스텍 내부 값 확인
	bool isempty();						// 스텍이 비어있는지 확인
};

Stack::Stack(int size = 3)				// 스텍 크기 기본 3 설정
{
	N = size;
	stack = new int[N];					// 스텍 메모리 동적 할당
	top = -1;							// top 을 -1로 설정 0부터 데이터 존재
}

Stack::~Stack()
{
	delete[] stack;						// 동적할당으로 얻은 메모리 공간 반납
}

bool Stack::isempty()
{
	return top == -1;					// top 이 -1 일 경우 스텍이 비어있음
}

void Stack::push(int value)
{
	if (top == (N - 1))					// top 이 N-1 까지 가있으면 데이터가 full임을 의미 
		cout << "stack is full" << endl;
	else
		stack[++top] = value;			// full 이 아니면 다음 공간에 데이터 저장

}

int Stack::read_top()
{
	cout << "top value : " << top << endl;
	return top;							// top 값을 반환
}

void Stack::pop()
{
	if (isempty())						// 스텍이 비어 있으면 pop 할 데이터가 없으므로 메시지 출력
		cout << "stack is empty" << endl;
	else
		top--;							// 데이터 하나 출력되어 top 내림
}
void Stack::check_stack()
{
	if (top > -1) {						// 스텍이 비어 있지 않으면 데이터 하나씩 열람 
		for (int i = 0; i < top + 1; i++)
			cout << stack[i] << " ";
		cout << endl;
		cout << "Total number for data is " << (top + 1);

		cout << endl;
		read_top();
		cout << endl;
	}
}

int main() {
	Stack st;							// 스텍 인스턴스 생성, 초기 값 안 줬으므로 스텍 크기는 3

	st.pop();
	st.push(5);
	st.check_stack();
	st.push(9);
	st.check_stack();
	st.push(4);
	st.check_stack();
	st.push(7);							// stack is full
	st.pop();
	st.check_stack();
	st.pop();
	st.check_stack();
	st.pop();
	st.check_stack();
	st.pop();							// stack is empty
	st.check_stack();

}
```
# Stack & Queue
## 2.Queue 
### - Example 4 
```c++
#include <iostream>

using namespace std;

class Queue {
private:
	int* queue;
	int front, rear;
	int capacity;
	bool is_empty() const;
public:
	Queue(int N);
	~Queue();
	void push(const int data);
	void pop();
	void read_front() const;
	void read_rear() const;
	void check_queue() const;

};

Queue::Queue(int N = 10)
{
	capacity = N;
	queue = new int[capacity];
	front = 0;
	rear = 0;
}

Queue::~Queue() {
	delete[] queue;
}

void Queue::push(const int data)
{
	if ((rear - front) == -1 || (rear - front == capacity - 1))
		cout << "queue is full" << endl;
	else
	{
		rear++;
		if (rear == capacity)
			rear = 0;
		queue[rear] = data;
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
		front++;
		if (front == capacity)
			front = 0;
		cout << "pop data is " << queue[front] << endl;
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
			cout << queue[i] << " ";
		cout << endl;
		cout << "Total number of data is " << (rear - front);


	}
	else {
		for (int i = front + 1; i < capacity; i++)
			cout << queue[i] << " ";
		for (int i = 0; i < rear + 1; i++)
			cout << queue[i] << " ";
		cout << endl;
		cout << "Total number of data is " << (10 + rear - front);
	}
	cout << endl;
	read_front();
	read_rear();
	cout << endl;
}

int InputDataCheck(int selection)
{
	while ((selection != 1) && (selection != 2) && (selection != 3)) {
		cout << "Selection number error , selection number shold be within [1, 2, 3]" << endl;
		cout << "Select new number " << endl;
		cin >> selection;
		cout << endl;
	}
	return selection;
}

void main()
{
	Queue q;
	int i32test_sel_num = 1;
	int i32push_pop, i32data;

	while (i32test_sel_num == 1) {
		cout << "How do you want to test the queue!" << endl << "1. Push" << endl << "2. Pop" << endl << "3. End test" << endl;
		cout << "please select the number : " << endl;
		cin >> i32push_pop;
		i32push_pop = InputDataCheck(i32push_pop);

		if (i32push_pop == 1) {
			cout << "please input the data: ";
			cin >> i32data;
			cout << endl;
			q.push(i32data);
			q.check_queue();
		}
		else if (i32push_pop == 2) {
			q.pop();
			q.check_queue();
		}
		else if (i32push_pop == 3) {
			i32test_sel_num = 0;
		}
	}
}
```
### - Task 1
```c++
#include <iostream>

using namespace std;

class MultiStack {
private:
	int N;								
	int* stack;							
	int top;							
public:
	MultiStack(int size);					
	~MultiStack();							
	void push_floor(int* value);				
	void push_ceil(int* value);
	void pop(int n);
	void pop();
	int read_top();						
	void check_stack();					
	bool isempty();						
};
int main()
{
	MultiStack st(2);

	int a[3];
	a[0] = 1;
	a[1] = 2;
	a[2] = 3;
	st.push_ceil(a);
	st.pop();
	st.pop(2);
	st.push_floor(a);
}


```
### - Task 2
```c++
#include<iostream>

using namespace std;

class Customer {
private:
	string name;
	bool data;
public:
	Customer(string _name="None")
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

int main() {
	Customer c1("jake"), c2("grace"), c3("dave"), c4("peter"), c5("youjean");
	Queue q;

	q.push(&c1);
	//q.check_queue();
	q.push(&c2);
	//q.check_queue();
	q.push(&c3);
	//q.check_queue();
	q.push(&c4);
	//q.check_queue();
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
	
	return 0;
}
```
