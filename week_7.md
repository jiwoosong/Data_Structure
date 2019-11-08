# Tree
## 1. Tree Traversal
### List Representation of Tree

```C++
#include <iostream>
using namespace std;

class Tree
{
	char data = NULL;
	Tree* left_child;
	Tree* right_sibling;
public:
	Tree(char _data)
	{
		left_child = NULL;
		right_sibling = NULL;
		this->data = _data;
	}
	void append_child_node(Tree* _child)
	{
		if (left_child == NULL) left_child = _child;
		else {
			Tree* temp = left_child;
			// fill the blank
		}
	}
	void print_tree(int _depth)
	{
		for (int i = 0; i < _depth; i++)
			cout << ' ';
		cout << data << endl;

		if (left_child != NULL) left_child->print_tree(_depth + 1);
		if (right_sibling != NULL) right_sibling->print_tree(_depth);
	}
};

int main() {
	Tree Root('A'), B('B'), C('C'), D('D'), E('E'), F('F');

	Root.append_child_node(&B);
	B.append_child_node(&C);
	B.append_child_node(&D);
	Root.append_child_node(&E);
	E.append_child_node(&F);

	Root.print_tree(0);

	return 0;
}
'''
