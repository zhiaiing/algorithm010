# 柠檬水找零

```
var lemonadeChange = function(bills) {
    var five = 0, ten = 0, len = bills.length;
    for (let i = 0; i < bills.length; i++) {
        if(bills[i] === 5) {
            five++;
        } else if(bills[i] === 10) {
            if(five === 0) {
                return false;
            };
            five--;
            ten++;
        } else if(bills[i] === 20) {
            if(ten >0 && five > 0) {
                ten--;
                five--;
            } else if(five >= 3) {
                five -= 3;
            } else {
                return false;
            }
        }
    }
    return true;
};
```



# 买卖股票的最佳时机 II

```
var maxProfit = function(prices) {
    let total = 0, length = prices.length;
    for(let i = 1; i < length; i++) {
        if (prices[i] > prices[i-1]) {
            total += prices[i] - prices[i-1];
        }
    }
    return total;
};
```



# 分发饼干
```
var findContentChildren = function(g, s) {
    g = g.sort((a, b) => a - b);
    s = s.sort((a, b) => a - b);

    let conunt = 0;
    for(let i=0, j=0; i<g.length && j<s.length;) {
        if (g[i] <= s[j]) {
            conunt++;
            i++;
        } 
         j++;
    }
    return conunt;
};
```



# 模拟行走机器人

```
var robotSim = function(commands, obstacles) {
      var dx = [0,1,0,-1];
    var dy = [1,0,-1,0];
    var di = 0;
    var endX = 0;
    var endY = 0;
    var result = 0;
    var hashObstacle = {};
    for(var r = 0;r<obstacles.length;r++){
        hashObstacle[obstacles[r][0]+'-'+obstacles[r][1]] = true;
    }
    for(var s = 0;s<commands.length;s++){
        if(commands[s] == -2){
            di = (di+3)&3;
        }else if(commands[s] == -1){
            di = (di+1)&3;
        }else{
            // 每次走一步
            for(var z = 1;z <= commands[s];z++){
                var nextX = endX + dx[di];
                var nextY = endY + dy[di];
                // 判断下一步是否为障碍物
                if(hashObstacle[nextX+'-'+nextY]){
                    break;
                }
                endX = nextX;
                endY = nextY;
                result = Math.max(result,endX*endX+endY*endY);
            }
        }
    }
    return result;
}
```



# 词接龙

```
var ladderLength = function(beginWord, endWord, wordList) {
    let wordListSet = new Set(wordList);
    if(!wordListSet.has(endWord)){
        return 0;
    }
    let beginSet = new Set();
    beginSet.add(beginWord);
    let endSet = new Set();
    endSet.add(endWord)
    let level = 1;
    while (beginSet.size > 0) {
        let next_beginSet = new Set();
        for(let key of beginSet){
            for(let i = 0;i < key.length;i++){
                for(let j = 0;j < 26;j++){
                   let s =  String.fromCharCode(97+j);
                   if(s != key[i]){
                        let new_word = key.slice(0,i)+s+key.slice(i+1);
                        if(endSet.has(new_word)){
                            return level + 1;
                        }
                        if(wordListSet.has(new_word)){
                            next_beginSet.add(new_word);
                            wordListSet.delete(new_word);
                        }
                   }
                }
            }
        }
        beginSet = next_beginSet;
        level++;
        if(beginSet.size > endSet.size){
            [beginSet,endSet] = [endSet,beginSet]
        }
    }
    return 0;
};
```



# 岛屿数量

```
var DFS = function(grid, i, j) {
    if (i < 0 || j < 0 || i >= grid.length || j >=grid[i].length || grid[i][j] === '0') return;
    grid[i][j] = '0';
    DFS(grid, i-1, j);
    DFS(grid, i+1, j);
    DFS(grid, i, j-1);
    DFS(grid, i, j+1);
}

var numIslands = function(grid) {
    let length = grid.length, count = 0;
    for(let i = 0; i < length; i++) {
        let item = grid[i];
        let length1 = item.length; 
        for(let j = 0; j < length1; j++) {
            if (item[j] === '1') {
                count++;
                DFS(grid, i, j);
            }
        }
    }

    return count;
};
```



# 跳跃游戏

```
var canJump = function(nums) {
    if (!nums.length) return true
    let dis = nums.length - 1
    for (let i = nums.length - 1; i >= 0; i--) {
        if (nums[i] + i >= dis) {
            dis = i
        }
    }
    return dis === 0 
};
```


# 搜索旋转排序数组

```
var search = function(nums, target) {
    let l = 0
  let r = nums.length - 1
  while(l <= r){
    let mid = l + ((r - l) >> 1)         
    if(nums[mid] === target) return mid 
    if(nums[l] <= nums[mid]){
      if(nums[mid] > target && nums[l] <= target){  
        r = mid - 1
      } else {  // 否则处于 [mid + 1, r]中
        l = mid + 1
      }
    } else {                          
      if(nums[mid] < target && nums[r] >= target){   
        l = mid + 1
      } else {  
        r = mid - 1
      }

    }
  }

  return -1;
};
```



# 跳跃游戏 II
var jump = function(nums) {
    let steps = 0, end = 0, len = nums.length, max = 0;

    for (let i = 0; i < len - 1; i++) {
        max = Math.max(max, i + nums[i]);
        if (max >= len -1) return ++steps;
        if (i === end) {
            end = max;
            steps++;
        }
    } 
    return steps;
};