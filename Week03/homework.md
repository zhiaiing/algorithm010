# 二叉树的最近公共祖先

```
var lowestCommonAncestor = function(root, p, q) {
    if (root===null||root===p||root===q) {
        return root
    }
    let left = lowestCommonAncestor(root.left, p, q)
    let right = lowestCommonAncestor(root.right, p, q)
    if (left && right) {
        return root
    }
    return left ? left : right
}
```



# 从前序与中序遍历序列构造二叉树

```
var buildTree = function(preorder, inorder) {
    var pre = 0, i = 0;
    function build(stop) {
        if (inorder[i] != stop) {
            var root = new TreeNode(preorder[pre++])
            root.left = build(root.val)
            i++;
            root.right = build(stop)
            return root
        }
        return null
    }
    return build()
};
```



# 组合

```
var getValue = function(currunt, max, curruntResult, result, rest, total) {
    if (rest === 0) {
        if (curruntResult.length === total) result.push(curruntResult);
        return;
    }
    currunt++;
    rest <= (max - currunt) && getValue(currunt, max, curruntResult, result, rest, total);
    getValue(currunt, max, [...curruntResult, currunt], result, --rest, total);
}

var combine = function(n, k) {
    let result = [];
    getValue(0, n, [], result, k, k);
    return result;
};
```



# 全排列

```
var getValue = function(newNums, currunt, curruntResult, result) {
    let length = newNums.length,length1 = curruntResult.length;
    if (length1 === length) {
        result.push(curruntResult);
        return;
    }

    for(let i = length1; i < length; i++) {
        const newArray = [...newNums];
        newArray[length1] = newArray[i];
        newArray[i] = newNums[length1];
        getValue(newArray, i + 1,[...curruntResult, newNums[i]], result)
    }
}

var permute = function(nums) {
    let result = [];
   getValue(nums, 1, [], result);
   return result;
};
```



# 全排列 II

```
var swap = function(nums, i, j) {
    if (i === j) return;
    const t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
};

var cal = function (nums, first, result) {
    if (nums.length === first) {
        result.push([...nums]);
        return;
    }
    const map = new Map();
    for (let i = first; i < nums.length; i++) {
        if (!map.get(nums[i])) {
            map.set(nums[i], true);
            swap(nums, first, i);
            cal(nums, first + 1, result);
            swap(nums, first, i);
        }
    }
};

/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function(nums) {
    if (nums == null) return;
    const res = [];
    cal(nums, 0, res);
    return res; 
};
```