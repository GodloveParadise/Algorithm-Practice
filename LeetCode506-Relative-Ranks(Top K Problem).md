> 
> LeetCode506 Relative Ranks  
>
> 题目：  
> Given scores of N athletes, find their relative ranks and the people
     with the top three highest scores,who will be awarded medals:
     "Gold Medal", "Silver Medal" and "Bronze Medal".
>  


> 思想：从N个数中寻找最大的K个数，利用最小堆实现。
```
void AdjustDown(vector<int> &scores, vector<int> &heap, int index, int size)
{
	int temp = heap[index];
	for (int ii = 2 * index + 1; ii <= size; ii *= 2)
	{
		if (ii<size&& scores[heap[ii]]>scores[heap[ii + 1]])
		{
			ii++;
		}

		if (scores[temp]>scores[heap[ii]])
		{
			heap[index] = heap[ii];
			index = ii;
		}
		else
		{
			break;
		}
	}
	heap[index] = temp;
}
void BuildMinHeap(vector<int> &scores, vector<int> &heap)
{
	int mid = (heap.size()) / 2;
	for (int ii = mid; ii >= 0; ii--)
	{
		AdjustDown(scores, heap, ii, heap.size() - 1);
	}

}
void HeapSort(vector<int>  &scores, vector<int> &heap)
{
	int temp;
	for (int ii = 0; ii < heap.size(); ii++)
	{
		temp = heap[0];
		heap[0] = heap[heap.size() - 1 - ii];
		heap[heap.size() - 1 - ii] = temp;
		AdjustDown(scores, heap, 0, heap.size() - ii - 1);
	}
}
void TopK(vector<int>  scores, int topK)
{
	vector<int> heap;
	for (int ii = 0; ii < topK; ii++)
	{
		heap.push_back(ii);
	}
	BuildMinHeap(scores, heap);
	cout << "build";
	for (int ii = topK; ii < scores.size(); ii++)
	{
		if (scores[ii]>scores[heap[0]])
		{
			heap[0] = ii;
			AdjustDown(scores, heap, 0, heap.size() - 1);
		}
	}

	HeapSort(scores, heap);
	//输出
	for (int ii = 0; ii < topK; ii++)
	{
		cout << heap[ii] << "  ";
	}

}
```
