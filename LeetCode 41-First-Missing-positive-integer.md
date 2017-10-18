> 
> 思想：
>    1.遍历数组，将N交换到num[N]处，当num[N]<0或者num[N]>num.size()时不交换
>    2.再次遍历数组，当N！=num[N]时即是第一个缺少的整数
> 测试用例： [1,1]
> 

```
void swap(int &a, int &b)
{
	a = a + b;
	b = a - b;
	a = a - b;

}
int firstMissingInteger(vector<int> nums)
{
	if (nums.size() < 1)
		return 1;
	for (int ii = 0; ii < nums.size(); ii++)
	{

		if (nums[ii]>0 && nums[ii] != ii+1 && nums[ii] < nums.size())
		{
			if (nums[ii] != nums[nums[ii] - 1])
			{
				swap(nums[ii], nums[nums[ii] - 1]);
				ii--;
			}
		}
	}

	for (int ii = 0; ii < nums.size(); ii++)
	{

		if (nums[ii] != ii+1)
		{
			return ii+1;
		}
	}

	return nums.size() + 1;
}
```
