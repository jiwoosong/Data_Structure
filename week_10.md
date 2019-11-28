
# Sorting
## 1. Bubble insertion sort
```C++
#include<iostream>
using namespace std;

int DataArray[10] = { 0 };

void BubbleSort(int *DataArray, int Length)
{
	for (int i = 0; i < Length - 1; i++)
	{
		//가장 오른쪽의 원소 두 개는 비교하지 않아도 된다.
		for (int j = 0; j < Length - (i + 1); j++)
		{
			//왼쪽이 오른쪽보다 크면
			if (DataArray[j]>DataArray[j + 1]) 
				swap(DataArray[j + 1], DataArray[j]);
		}
	}
}

void InsertionSort(int *DataArray, int Length)
{
	for (int i = 1; i < Length; i++)
	{
		// 방법(1) (방법1,2 둘중 하나를 주석처리 하세요)
		// 정렬할 필요성이 없다면 한 회 넘어간다.
		if (DataArray[i - 1] <= DataArray[i]) continue;
		// 정렬할 필요가 있으면 i 번째 데이터를 value 에 넣어둔다.
		int value = DataArray[i];
		// value 보다 큰 요소를 찾아내기위해 왼쪽부터 다시 검색한다.
		for (int j = 0; j < i; j++)
		{
			// value 보다 큰 요소를 찾아낸다.
			if (DataArray[j] > value)
			{
				// 여기서 memmove 함수는 메모리 블럭을 옮기는 함수입니다.
				// 아래 문장을 해석하면, &arrData[j] 부터 sizeof(arrData[0]) * (i-j)만큼 &arrData[j+1]로 이동한다는 말입니다.
				memmove(&DataArray[j + 1], &DataArray[j], sizeof(DataArray[0]) * (i - j));
				DataArray[j] = value;
				break;
			}
		}

		// 방법(2)
		int key = DataArray[i];
		int j = i - 1;
		//왼쪽 데이터가 오른쪽 데이터보다 크다면
		while (j >= 0 && key < DataArray[j])
		{
			//왼쪽과 오른쪽을 바꾼다.
			swap(DataArray[j], DataArray[j + 1]);
			j--;//왼쪽을 다시확인하기위해
		}
	}
}

void swap(int &i, int &j)
{
	int temp = i;
	i = j;
	j = temp;
}

void print()
{
	for (int i = 0; i < 10; i++)
		cout << DataArray[i] << " ";
	cout << endl;
}

void main()
{
	//난수배열 만들기
	for (int i = 0; i < 10; i++)
		DataArray[i] = rand() % 20;

	print();
	InsertionSort(DataArray, 10);
	print();

	//난수배열 만들기
	for (int i = 0; i < 10; i++)
		DataArray[i] = rand() % 20;

	print();
	BubbleSort(DataArray, 10);
	print();
}

```
## 2. Quick Sort
```C++
#include<iostream>
using namespace std;

void print(int *A)
{
	for (int i = 0; i < 8; i++)
		cout << A[i] << " ";
	cout << endl;
}

int Partition(int *A, int start, int end)
{
	int pivot = A[end];//가장 마지막을 피벗으로
	//pivot 보다 작은 요소의 위치를 바꿀 index
	int partitionIndex = start;
	for (int i = start; i < end; i++)
	{
		//pivot보다 작으면 왼쪽으로 하나 씩 보낸다
		if (A[i] <= pivot)
		{
			...
      			...
			print(A);
		}
	}
	//pivot 보다 작은 값을 왼쪽에 위치시킨후 이므로
	//그 다음 값은 pivot이 위치해야한다.
	...
	print(A);
	//Index를 return하여 다음 pivot을 어디로 할지 정할 수 있다.
	return partitionIndex;
}

//start 부터 end 까지 정렬시킨다.
void QuickSort(int *A, int start, int end)
{
	if (start < end) //start >= end 인 경우는 정렬이 다 된 상황.
	{
		int partitionIndex = Partition(A, start, end);
		QuickSort(A, start, partitionIndex - 1);//피벗의 왼쪽
		QuickSort(A, partitionIndex + 1, end);//피벗의 오른쪽
	}
}

void main()
{
	int A[] = {7, 2, 1, 6, 8, 5, 3, 4};
	
	QuickSort(A, 0, 7);

	print(A);
}

```
## 2. Merge Sort
```C++
#include<iostream>
#include<time.h>

#define N 10 // 배열의 크기
int tmp[N];//병합을 위한 임시배열
using namespace std;

void print(int *arr)
{
	for (int i = 0; i < N; i++)
		cout << arr[i] << " ";
	cout << endl << endl;
}

void ArrayMerge(int start, int end, int* arr)//두 배열의 병합함수
{
	int mid = (start + end) / 2;//반으로 나눴을 때, 첫번째 배열의 끝 인덱스

	int i = start; //첫번째 배열의 시작 인덱스
	int j = mid + 1;//두번째 배열의 시작 인덱스

	int k = start; //임시배열의 시작 인덱스
	while (...)//두 배열의 끝에 이르기까지 반복
	{
		if (arr[i] <= arr[j]) //첫번째 배열의 원소가 두번째 배열 원소보다 더 작거나 같으면
		{
			...//임시배열에 첫번째 배열 원소 추가
			...//첫번째 배열 현재 인덱스 +1
		}
		else//두번째 배열의 원소가 더 작거나 같으면
		{
			...//임시배열에 두번째 배열 원소 추가
			...//두번째 배열 현재 인덱스 +1
		}
		k++; //임시배열의 현재 인덱스 +1 
		print(arr);
	}

	//두 배열을 비교하고 남은 원소들을 임시배열에 추가
	//기존 arr 배열에 추가하면 원래 정보가 업데이트 되어버림

	int t;      //추가할 원소가 남은 배열의 시작 인덱스
	if (i > mid) //첫번째 배열의 원소가 모두 추가되었으면
		t = j; //시작 인덱스를 두번째 배열의 현재 인덱스로 설정
	else       //두번째 배열의 원소가 모두 추가되었으면
		t = i;//시작 인덱스를 첫번째 배열의 현재 인덱스로 설정

	//남은 원소들을 임시배열에 추가
	for (k; k <= end; k++, t++)
		tmp[k] = arr[t];
	//임시배열에서 원래 배열로 복사
	for (k = 0; k <= end; k++)
		arr[k] = tmp[k];
	print(arr);
}

void MergeSort(int start, int end, int*arr)
{
	int mid;
	if (start < end)
	{
		mid = (start + end) / 2; //배열의 중간 인덱스
		MergeSort(start, mid, arr);//왼쪽 배열 분할
		MergeSort(mid + 1, end, arr);//오른쪽배열 분할
		ArrayMerge(start, end, arr);//병합
	}
}

void main()
{
	srand(time(NULL));
	int arr[N];

	//랜덤배열 생성
	for (int j = 0; j < N; j++)
		arr[j] = rand() % 100 + 1;

	print(arr);

	//병합정렬 실행
	MergeSort(0, N - 1, arr);

	//실행 후 배열 출력
	print(arr); 
	
	cout << endl;
	return;
}
```
