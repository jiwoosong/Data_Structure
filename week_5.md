# Stack & Queue
## 1.Stack 
### - Example 1 
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
## 1.Queue 
### - Example 2 
