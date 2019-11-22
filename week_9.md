# Graph [Adjacency list, Searching methods]
## 1. Tree Traversal
```C++
#include <iostream>
using namespace std;
struct AdjListNode		//(adjacency list를 위한) 노드 자료형 만들기
{
	//노드의 data
	int data;
	//또 다른 노드를 가리키기 위한 포인터변수
	struct AdjListNode* next;
};
struct AdjList			//adjacency list 자료형 만들기
{
	//list에서 head 노드를 가리키기 위한 포인터변수
	struct AdjListNode *head;
};
```

```C++
class Graph
{
private:
	int V;//V는 노드의 개수
	struct AdjList* array;//첫번째 노드가 다른, 리스트들을 표현하기위한 포인터배열

public:
	Graph(int V)	//노드의 개수를 인자로 받음
	{
		this->V = V;
		array = new AdjList[V];	//노드의 개수만큼 list 생성
		
		for (int i = 0; i < V; ++i) //모든 리스트들의 head 값을 NULL로 초기화
			array[i].head = NULL;
	}

	void DFS(int node) //node는 탐색을 시작할 위치를 뜻한다.
	{
		
		bool *state = new bool[V]; // state라는 배열을 만들어 방문여부를 체크할 수 있도록 한다.
		for (int i = 0; i < V; i++) // state 배열을 false로 초기화 시킨다.
			state[i] = false;
		cout << "DFS 방식" << endl;
		runDFS(node, state, array[node].head);
		cout << endl;
	}
	//전체적인 구성은 모든 인접리스트들을 돌아보고,
	//인접리스트들을 돌아보는 도중 방문 안한 노드가 있으면
	//그 노드로 들어가서 탐색을 한다.
	//DFS를 실행할 재귀함수
	void runDFS(int node, bool state[], AdjListNode* temp)
	{
		//Node에 들어왔으므로 해당 노드의 state는 True로 변경한다.
		...
		//인접리스트들을 모두 탐색한다.
		...
		while (...){
			//state가 0이면 방문하지 않았다는 것이므로 재귀함수를 시작한다.
			...
			//state = 1이면 탐색이 되었던 노드이므로 인접노드를 확인한다.
			...
		}
	}

	//새로운 노드를 만들고 그 노드의 주소값을 반환하는 함수 정의
	AdjListNode* newAdjListNode(int data)
	{
		//new AdjListNode;	=	노드의 이름은 newNode
		//new AdjListNode	=	AdjListNode 형식으로 생성
		//AdjListNode*		=	노드의 주소값을 반환
		AdjListNode* newNode = new AdjListNode;
		newNode->data = data;
		newNode->next = NULL;
		return newNode;
	}
  
  void addEdge(int src, int data)
	{
		//노드를 가리키는 포인터 newNode는 새로 만들어진 노드를 가리킨다.
		AdjListNode* newNode = newAdjListNode(data);//'data'가 들어간 노드
		newNode->next = array[src].head;
		array[src].head = newNode;

		newNode = newAdjListNode(src);
		newNode->next = array[data].head;
		array[data].head = newNode;
	}

	//두 노드를 서로 연결시키는 함수
	void Directed_addEdge(int src, int data)
	{
		//노드를 가리키는 포인터 newNode는 새로 만들어진 노드를 가리킨다.

		/*
			Write down your own code
		*/
	}


	//그래프 출력
	void printGraph()
	{
		for (int i = 0; i < V; ++i)	//노드의 개수만큼 출력
		{
			//list들의 head가 가진 주소값을 pCrawl에 하나씩 대입
			AdjListNode* pCrawl = array[i].head;
			cout << "\n Adjacency list of vertex " << i << "\n head ";
			while (pCrawl)//NULL일때 까지 반복하기위해
			{
				cout << "-> " << pCrawl->data;
				pCrawl = pCrawl->next;
			}
			cout << endl;
		}
		cout << "------------------------------------" << endl;
	}
};
```
### Build graph main
```C++
int main()
{
	Graph gh(7);

	gh.addEdge(0, 1);
	gh.printGraph();
	gh.addEdge(0, 3);
	gh.printGraph();
	gh.addEdge(0, 6);
	gh.printGraph();
	gh.addEdge(1, 2);
	gh.printGraph();
	gh.addEdge(1, 4);
	gh.printGraph();
	gh.addEdge(1, 5);
	gh.printGraph();
	gh.addEdge(1, 6);
	gh.printGraph();
	gh.addEdge(3, 4);
	gh.printGraph();
	gh.addEdge(3, 6);
	gh.printGraph();
	gh.addEdge(4, 5);
	gh.printGraph();
  
	return 0;
}
```

### Build graph
#### Undirected Graph
```C++
int main()
{
	Graph gh(7);

	gh.addEdge(0, 1);
	gh.printGraph();
	gh.addEdge(0, 3);
	gh.printGraph();
	gh.addEdge(0, 6);
	gh.printGraph();
	gh.addEdge(1, 2);
	gh.printGraph();
	gh.addEdge(1, 4);
	gh.printGraph();
	gh.addEdge(1, 5);
	gh.printGraph();
	gh.addEdge(1, 6);
	gh.printGraph();
	gh.addEdge(3, 4);
	gh.printGraph();
	gh.addEdge(3, 6);
	gh.printGraph();
	gh.addEdge(4, 5);
	gh.printGraph();
  
	return 0;
}
```
#### Directed Graph
```C++
int main()
{
	Graph gh(7);

	gh.Directed_addEdge(0, 1);
	gh.printGraph();
	gh.Directed_addEdge(0, 3);
	gh.printGraph();
	gh.Directed_addEdge(0, 6);
	gh.printGraph();
	gh.Directed_addEdge(1, 2);
	gh.printGraph();
	gh.Directed_addEdge(1, 4);
	gh.printGraph();
	gh.Directed_addEdge(1, 5);
	gh.printGraph();
	gh.Directed_addEdge(1, 6);
	gh.printGraph();
	gh.Directed_addEdge(3, 4);
	gh.printGraph();
	gh.Directed_addEdge(3, 6);
	gh.printGraph();
	gh.Directed_addEdge(4, 5);
	gh.printGraph();
  
	return 0;
}
```
#### DFS <TASK 1>
```C++
int main()
{
	Graph gh(7);

	gh.addEdge(0, 1);
	gh.printGraph();
	gh.addEdge(0, 3);
	gh.printGraph();
	gh.addEdge(0, 6);
	gh.printGraph();
	gh.addEdge(1, 2);
	gh.printGraph();
	gh.addEdge(1, 4);
	gh.printGraph();
	gh.addEdge(1, 5);
	gh.printGraph();
	gh.addEdge(1, 6);
	gh.printGraph();
	gh.addEdge(3, 4);
	gh.printGraph();
	gh.addEdge(3, 6);
	gh.printGraph();
	gh.addEdge(4, 5);
	gh.printGraph();
  
  gh.DFS(5)
	return 0;
}
```
```C++
int main()
{
	Graph gh(7);

	/*
  BUild graphs
  */
  
  gh.DFS(5)
	return 0;
}
```
