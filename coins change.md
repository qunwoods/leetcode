# coins change
#LeetCode   #背包问题   

描述：数组中存在各种面值的硬币，可重复使用，求使得和为target的组合最短的数是多少

思路：使用dfs超时了，未解决（背包问题）

```python
import sys

class Solution:
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
        if amount == 0:
            return 0

        self.map = dict()

        self.res = self.dfs(coins, amount)
        
        return -1 if self.res == sys.maxsize else self.res

    def dfs(self, coins, target):

        key = tuple(coins + [target])

        if key in self.map:
            return self.map[key]

        if target == 0:
            self.map[key] = 0
            return self.map[key]

        if (target >= 0 and len(coins) <= 0) or target < 0:
            return sys.maxsize

        self.map[key] = min(self.dfs(coins, target - coins[0]) + 1, self.dfs(coins[1:], target))
        
        return self.map[key]

```