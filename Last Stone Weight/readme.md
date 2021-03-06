We have a collection of stones, each stone has a positive integer weight.

* Each turn, we choose the two heaviest stones and smash them together.  Suppose the stones have weights x and y with x <= y.  The result of this smash is:

* If x == y, both stones are totally destroyed;
* If x != y, the stone of weight x is totally destroyed, and the stone of weight y has new weight y-x.
* At the end, there is at most 1 stone left.  Return the weight of this stone (or 0 if there are no stones left.)

 

## Example 1:

	Input: [2,7,4,1,8,1]
	Output: 1
	Explanation: 
	We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
	we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
	we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
	we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of last stone.
 

## Note:

* 1 <= stones.length <= 30
* 1 <= stones[i] <= 1000

## [原題目連結點我](https://leetcode.com/problems/last-stone-weight/)
	
## 我的心得:
* main.py
* 先 sort 好，就可以 pop 出兩個最大的
* 之後再依據題意做判斷
* 要注意的是 `x != y` 時，因為會產生新的數值放回去，就使用插入放入就好，因為相減的數通常是小的，從小的數值開始比對決定要在哪插入會有較少的 iteration
-----

* 我在討論區看到不錯的用法(是直接使用 API 的，有空我來刻演算法看看)
```python
import heapq
class Solution:
	    def lastStoneWeight(self, stones: List[int]) -> int:
		stones = [-val for val in stones]
		heapq.heapify(stones)
		while len(stones) > 1:
		    x1 = heapq.heappop(stones)
		    x2 = heapq.heappop(stones)
		    if x1 != x2:
			heapq.heappush(stones,x1-x2)
		if len(stones) == 0:
		    return 0
		return -stones[0]
```
* 在 python 這個 API 當中，是用 min heap，也就是說 parent node 會小於 child node，故樹上最小的元素永遠會在根節點 heap[0]
* 所以 `heappop` 會"傳回 heap 中最小的元素"
* 第二次的 `heappop` 依舊會"傳回 heap 中最小的元素"
