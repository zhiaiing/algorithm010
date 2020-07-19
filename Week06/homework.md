# 最小路径和

```
var minPathSum = function(grid) {
    let m = grid.length, n = grid[0].length;
    for(let i = m-1; i >=0; i--) {
        for(let j = n-1; j >=0; j--) {
            if ((i === m -1 && j === n-1)) {
                grid[i][j] = grid[i][j];
            } else {
                grid[i][j] = Math.min(j+1 >= n ? Infinity : grid[i][j+1], i+1 >= m ? Infinity : grid[i+1][j])+ grid[i][j]
            }
        }
    }
    return grid[0][0]
};
```


# 解码方法

```
var numDecodings = function(s) {
    if (!s) return 0
    let len = s.length;
    let dp =  Array(len + 1).fill(0);
    dp[0] = 1;
    dp[1] = s[0] === '0' ? 0 : 1;
    for (let i = 2; i <= len; i++) {
        if (s[i - 1] !== '0') {
            dp[i] += dp[i - 1];
        }
        if (s[i - 2] === '1' || (s[i - 2] === '2' && s[i - 1] >= 0 && s[i - 1] <= 6)) {
            dp[i] += dp[i - 2];
        }
    }
    return dp[len];
};
```


# 最大正方形

```
var maximalSquare = function(matrix) {
  if (matrix.length === 0) return 0;
  const rows = matrix.length, cols = matrix[0].length;
  let max = 0;
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
        if (matrix[i][j] === '1') {
            matrix[i][j] = Math.min(i-1 < 0 ? 0 :matrix[i-1][j], (i-1 < 0 ||  j -1 < 0)  ? 0 : matrix[i-1][j-1], j - 1 < 0 ? 0 : matrix[i][j-1]) + 1;
            max = Math.max(max, matrix[i][j]);
        } 
            
    }
  }
  return max*max;
};
```


# 回文子串

```
var countSubstrings = function(s) {
   let n = s.length, dp = Array.from(new Array(n), () => new Array(n).fill(false)), result = 0;
   for(let i = 0; i < n; i++){
      for(let j = i; j >= 0; j--){
        if(s[i] == s[j] && (i - j < 2 || dp[i-1][j+1])){
            dp[i][j] = true
            result++
        }
      }
   }
   return result
};
```

# 最长有效括号

```
let maxLen = 0;
  const len = s.length, dp = new Array(len).fill(0);
  for (let i = 1; i < len; i++) {
    if (s[i] == ')') {
      if (s[i - 1] == '(') {
        if (i - 2 >= 0) {
          dp[i] = dp[i - 2] + 2;
        } else {
          dp[i] = 2;
        }
      } else if (s[i - dp[i - 1] - 1] == '(') {
        if (i - dp[i - 1] - 2 >= 0) {
          dp[i] = dp[i - 1] + 2 + dp[i - dp[i - 1] - 2];
        } else {
          dp[i] = dp[i - 1] + 2;
        }
      }
    }
    maxLen = Math.max(maxLen, dp[i]);
  }
  return maxLen;
```


#  编辑距离

```
var minDistance = function(word1, word2) {
    let n = word1.length, m = word2.length, dp = [];
    for(let i = 0;i <= n;i++){
        dp.push([])
        for(let j = 0;j <= m;j++){
            if(i*j){
                dp[i][j] = word1[i-1] == word2[j-1]? dp[i-1][j-1]: (Math.min(dp[i-1][j],dp[i][j-1],dp[i-1][j-1]) + 1);
            }else{
                dp[i][j] = i + j;
            }
        }
    }
    return dp[n][m];
};
```