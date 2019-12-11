#Shortest Path & Priority Queue
## Shortest Path
```C++
//무방향 가중치
#include <iostream>
using namespace std;


struct Adjmatrix {
private:
	double **Adj;
	int len = 0;
	
	double *cost;
	int *path;
	bool * visited;
public:
	Adjmatrix(int _len) {
		len = _len;
		Adj = new double*[len];
		for (int i = 0; i < len; i++) {
			Adj[i] = new double[len];
			for (int j = 0; j < len; j++) Adj[i][j] = 0;
		}
		path = new int[len];
		cost = new double[len];
		visited = new bool[len];
		for (int i = 0; i < len; i++) { path[i] = -1; cost[i] = INFINITY; visited[i] = false; }
	}
	void set_index(int* arr) {

	}

	void addEdge(int V1, int V2, double weight) {
		// Update Adjacency matrix into weight value
		Adj[V1][V2] = weight;
		Adj[V2][V1] = weight;

	}

	void Dijkstra(int start) {
		cost[?] = 0;
		backtracking(?);
	}
	void backtracking(int V) {
		// Set V index's visited = true
		visited[V] = true;
		// Searching V index's connected nodes and update
		for (int i = 0; i < len; i++) {
			// Update weight of V's connected Node weight value (by adjacency matrix)
			double weight = ?
			// If weight is nonzero
			if (weight != 0) {
				// If (connected Node's cost) is bigger than (V's cost + weight)
				if (cost[i] > ?) {
					// Update path
					path[i] = ?;
					// Update Cost
					cost[i] = ?;
					// Cut Adjacency matrix
					Adj[V][i] = ?;
					Adj[i][V] = ?;
				}

			}
		}
		// Print Path & Cost table
		print_table(V, path, cost);

		// Find min cost index
		int index;
		double min_weight = INFINITY;
		for (int i = 0; i < len; i++) {
			if (cost[i] < min_weight) {
				// if Node has been visited, skip it!
				if (?) {
					index = i;
					min_weight = cost[i];
				}
			}
		}
		// Go Recursive function call
		if (!isinf(min_weight)) {
			backtracking(?);
		}
	}




	void print_table(int current, int*_path, double *_cost) {
		cout << endl << "( " << current << " )\t";
		for (int i = 0; i < len; i++) cout << "[" << i << "]\t";
		cout << endl << "Cost :\t";
		for (int i = 0; i < len; i++) if (!isinf(_cost[i]))cout << _cost[i] << "\t"; else cout << "\t";
		cout << endl << "Path :\t";
		for (int i = 0; i < len; i++) if (_path[i] != -1)cout << _path[i] << "\t"; else cout << "\t";
		cout << endl;
	}

};

void main() {

	/*
	// 이론 슬라이드
	Adjmatrix A(7);
	A.addEdge(0, 1, 2.0);
	A.addEdge(0, 4, 6.0);
	A.addEdge(0, 5, 16.0);
	A.addEdge(0, 6, 14.0);
	A.addEdge(1, 2, 8.0);
	A.addEdge(1, 3, 3.0);
	A.addEdge(1, 4, 7.0);
	A.addEdge(2, 6, 1.0);
	A.addEdge(3, 4, 4.0);
	A.addEdge(3, 5, 4.0);
	A.addEdge(3, 6, 10.0);
	A.addEdge(4, 5, 5.0);
	A.addEdge(5, 6, 3.0);
	A.Dijkstra(0, 6);*/

	// 실습 슬라이드
	Adjmatrix A(9);
	A.addEdge(0, 1, 3);
	A.addEdge(0, 3, 4);
	A.addEdge(0, 4, 8);
	A.addEdge(1, 2, 2);
	A.addEdge(1, 4, 4);
	A.addEdge(3, 4, 8);
	A.addEdge(3, 6, 3);
	A.addEdge(4, 7, 6);
	A.addEdge(4, 5, 5);
	A.addEdge(2, 5, 3);
	A.addEdge(7, 8, 2);
	A.addEdge(5, 8, 7);
	
	A.Dijkstra(0);
	
}

```

## priority Queue
```C++
// Priority Queue
#include <iostream>
using namespace std;

struct node
{
	int priority;
	string data;
	struct node *link;
};

class Priority_Queue
{
private:
	node *front;
public:
	Priority_Queue()
	{
		front = NULL;
	}


	//front의 값을 출력하고 
	void del()
	{
		node *tmp;
		if (front == NULL)
			cout << "Queue Underflow\n";
		else
		{
			tmp = front;
			cout << "Deleted Data is: " << tmp->data.c_str() << endl;
			front = front->link;//맨 앞을 가리키는 front를 다음으로 바꿈
			delete tmp;
		}
	}

	void insert(string item, int priority)
	{
		node *tmp, *q;
		tmp = new node;
		tmp->data = item;
		tmp->priority = priority;

		//삽입이 처음이거나 priority가 1순위보다 먼저면 바로 삽입 
		if (?)
		{
			?; //tmp의 next는 NULL
			?;//front를 새로들어온 tmp로 초기화
		}
		//삽입이 처음이 아니고 priority가 1순위보다 뒤면
		else
		{
			?;
			//첫번째부터 NULL일때 까지 검색하고 삽입할 priority가
			//검색하고있는 priority보다 크면 계속 뒤로 이동.
			while (?)
				?;
			//위의 while 문으로 priority의 적절한 위치를 찾으면 tmp를 중간에 연결
			?;
			?;
		}
	}


	void display()
	{
		cout << endl;
		node *ptr;
		ptr = front;
		if (front == NULL)
			cout << "	* Queue is empty\n";
		else
		{
			cout << "	* Queue\n";
			cout << "	Priority		Item\n";
			while (ptr != NULL)
			{
				cout << "	" << ptr->priority << "			" << ptr->data.c_str() << endl;
				ptr = ptr->link;
			}
		}
		cout << endl;
	}
	
};

void main()
{
	Priority_Queue pq;

	pq.insert("data1", 1);
	pq.insert("data2", 5);
	pq.insert("data3", 8);
	pq.insert("data4", 4);
	pq.insert("data5", 2);

	pq.display();

	pq.del();
	pq.del();

	pq.display();
}

```
