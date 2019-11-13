# BST
## 1. Tree Traversal
```C++

# include <iostream>
using namespace std;

class Node {
private:
	char data;
	Node* left;
	Node* right;
public:
	Node(char _data) { this->data = _data; left = NULL; right = NULL; }
	void set_left(Node* _left) { this->left = _left; }
	void set_right(Node* _right) { this->right = _right; }
	char get_data() { return data; }
	Node* get_left() { return left; }
	Node* get_right() { return right; }
};

class Tree {
private:
	Node* root;
public:
	Tree() { root = NULL; }
	Tree(Node* _root) { this->root = _root; }
	void new_root(Node* _root) { this->root = _root; }
	void preorder_print(Node* _leaf) // VLR
	{
		if (_leaf == NULL) return;
		// get_data를 활용해 데이터 출력
		cout << _leaf->get_data() << " ";
		// 왼쪽 탐색
		// 오른쪽 탐색
	}
	void inorder_print(Node* _leaf) // LVR
	{
	
	}
	void postorder_print(Node* _leaf) // LRV
	{
	
	}
};

void main()
{
	Node A('A'), B('B'), C('C'), D('D'), E('E'), F('F'), G('G'), H('H'), I('I');
	Tree tree(&A);

	A.set_left(&B);
	B.set_left(&D);
	D.set_left(&H);
	D.set_right(&I);
	B.set_right(&E);
	A.set_right(&C);
	C.set_left(&F);
	C.set_right(&G);

	cout << "preorder traversal" << endl;
	tree.preorder_print(&A);

	cout << endl << "inorder traversal" << endl;
	tree.inorder_print(&A);

	cout << endl << "postorder traversal" << endl;
	tree.postorder_print(&A);
	cout << endl;

}

```
## 2. BST implementation
```C++
#include <iostream>
using namespace std;

class Node {
	friend class Tree;
private:
	Node* left;
	Node* right;
	int data;
};

class Tree
{
private:
	Node* root;
public:
	Tree() { root = NULL; };
	Node* create_node(int _data);
	Node* search_node(Node* _current_node, int _find_data);
	Node* insert_node(Node* _current_node, int _input_data);
	Node* remove_node(Node* _current_node, int _find_data);
	Node* find_min_node(Node* _current_node);
	void print_tree(Node* _current_node);
};
Node* Tree::create_node(int _data)
{
	Node* new_node = new Node;
	if (root == NULL) root = new_node;
	new_node->data = _data;
	new_node->right = NULL;
	new_node->left = NULL;

	return new_node;
}

Node* Tree::search_node(Node* _current_node, int _find_data)
{
	if (_current_node == NULL) return NULL;
	if (_current_node->data == _find_data) return _current_node;
	else if (_current_node->data < _find_data)  // 찾으려는 데이터가 현재 노드의 데이터보다 작다면 
		search_node(_current_node->left, _find_data); // 왼쪽 자식 노드에서 탐색
	else
		search_node(_current_node->right, _find_data); // 반대의 경우는 오른쪽 자식 노드탐색
}

Node* Tree::insert_node(Node* _current_node, int _input_data)
{	// 새로 삽입되는 노드의 값이 현재 노드의 값보다 작다면 
	if (_current_node->data > _input_data)
	{
		// 현재 노드의 왼쪽 자식 노드가 있는지 확인한다. 
		if (_current_node->left != NULL)
			insert_node(_current_node->left, _input_data); // 왼쪽 자식 노드가 있다면 왼쪽 자식 부터 다시 insert 
		else
			_current_node->left = create_node(_input_data); // 자식 노드가 없다면 왼쪽 자식으로 creat_node
	}
	else if (_current_node->data < _input_data)
	{
		if (_current_node->right != NULL)
			insert_node(_current_node->right, _input_data);
		else
			_current_node->right = create_node(_input_data);
	}
	else
	{
		cout << "이미 같은 값의 노드가 존재합니다." << endl;
		return NULL;
	}
}

Node* Tree::find_min_node(Node* _current_node)
{
	if (_current_node == NULL) return NULL; // 현재노드가 없으면 NULL(실행될 일 없음 user failure)
	if (_current_node->left != NULL)return find_min_node(_current_node->left);
	else return _current_node;  // 현재 노드의 왼쪽자식이 없으면 _current_node 출력
}
Node* Tree::remove_node(Node* currentNode, int removeData)
{
	// 임시로 쓰일 노드 포인터
	Node* tempNode;

	// 현재 노드가 NULL이라는 것은 비어있는 것을 의미한다.
	if (currentNode == NULL) cout << "해당하는 노드를 찾을 수 없습니다." << endl;

	// 현재 노드의 값이 제거하려는 값보다 크다면, 왼쪽 자식 노드에서 제거하려는 값을 찾는다.
	else if (currentNode->data > removeData)
		//removeNode후 상위노드와의 관계를 설정하기위해 "currentNode->left = " 을 실행해둔다.
		
	// 현재 노드의 값이 제거하려는 값보다 작다면, 오른쪽 자식 노드에서 제거하려는 값을 찾는다.
	else if (currentNode->data < removeData)
		//removeNode후 상위노드와의 관계를 설정하기위해 "currentNode->right = " 을 실행해둔다.
		

	// 현재 노드의 값과 제거하려는 값이 같다면
	else //(currentNode->data == removeData)
	{
		// 현재 노드의 왼쪽 자식 노드와 오른쪽 자식 노드가 모두 있는 경우
		if (currentNode->left != NULL && currentNode->right != NULL)
		{
			// 현재 노드의 오른쪽 노드에서 가장 값이 작은 노드의 주소값이 tempNode에 들어간다.
			// 가장 값이 작은 노드는 제일 왼쪽에 있는 노드라고 생각하면 된다.
			
			// 현재 노드의 값에다 값이 가장 작은 노드의 데이터를 대입한다.
			
			// 현재 노드의 오른쪽 자식 노드에서 값이 가장 작은 노드를 제거한다.(위에서 대입됐으니까)
			
		}

		// 자식 노드가 없거나 한 쪽만 있는 경우
		else
		{
			// 임시 포인터 변수에다 지울 노드의 주소값을 대입한다.
			
			// 현재 노드의 왼쪽 자식 노드가 비어있으면, 현재 노드는 현재 노드의 오른쪽 자식 노드가 된다.
			if 
			// 현재 노드의 오른쪽 자식 노드가 비어있으면, 현재 노드는 현재 노드의 왼쪽 자식 노드가 된다.
			else if 
			// tempNode를 메모리에서 해제한다.
		}
	}
	// 현재 노드를 반환한다.
	
}

void Tree::print_tree(Node* _current_node)
{
	if (_current_node == NULL) return;

	print_tree(_current_node->left);
	cout << _current_node->data << " ";
	print_tree(_current_node->right);

}
void main()
{
	Tree A;
	Node* rootNode = A.create_node(15);

	A.insert_node(rootNode, 5);
	A.insert_node(rootNode, 8);
	A.insert_node(rootNode, 9);
	A.insert_node(rootNode, 12);
	A.insert_node(rootNode, 13);
	A.insert_node(rootNode, 17);
	A.insert_node(rootNode, 19);
	A.insert_node(rootNode, 20);

	A.print_tree(rootNode);
	cout << endl;

	A.remove_node(rootNode, 8);
	A.print_tree(rootNode);
	cout << endl;
	A.remove_node(rootNode, 19);
	A.print_tree(rootNode);
	cout << endl;
	A.remove_node(rootNode, 20);
	A.print_tree(rootNode);
	cout << endl;
}
```
