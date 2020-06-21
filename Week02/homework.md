# 有效的字母异位词

```
var isAnagram = function(s, t) {
    if (s.length !== t.length) return false;
    let length = s.length, obj = {};
    for(let i = 0; i < length; i++) {
        if (!obj[s[i]]) {
            obj[s[i]] = 1;
        } else {
            obj[s[i]] += 1;
        }

        if (!obj[t[i]]) {
            obj[t[i]] = -1;
        } else {
            obj[t[i]] -= 1;
        }
    }
    return !Object.keys(obj).some((key) => obj[key])

};
```



# 两数之和

```
var twoSum = function(nums, target) {
    let length = nums.length, obj = {};
    for(let i = 0; i < length; i++) {
        const differValue = target - nums[i];
        if (obj.hasOwnProperty(differValue)) {
            return [obj[differValue], i]
        } 
        obj[nums[i]] = i;
    }
    return [];
};
```



# N叉树的前序遍历

```
var preorder = function(root) {
    if (!root) return [];
    let result = [], arr = [root];

    while(arr.length) {
        var current = arr.pop();
        result.push(current.val);
         for(let i = current.children.length - 1; i >= 0; i--){
            arr.push(current.children[i]);
        }
    }
    return result;
};
```



# 字母异位词分组

```
var groupAnagrams = function(strs) {
    let hash = new Map()
    
    for(let i = 0; i < strs.length; i++) {
        let str = strs[i].split('').sort().join()
        if(hash.has(str)) {
            let temp = hash.get(str)
            temp.push(strs[i])
            hash.set(str, temp)
        } else {
            hash.set(str, [strs[i]])
        }
    }
    
    return [...hash.values()]
};
```

# 二叉树的中序遍历

```
var inorderTraversal = function(root) {
    let arr = []
    let stackArr = []
    while(root!=null || stackArr.length!=0){

        while(root!=null){
            stackArr.push(root)
            root = root.left
        }
        root = stackArr.pop()
        arr.push(root.val)
        root = root.right
    }
    return arr
};
```



# 二叉树的前序遍历

```
var preorderTraversal = function (root) {
    let stack = [root]
    let arr = []
    while (stack.length > 0) {
        let node = stack.pop();
        node && arr.push(node.val);
        node && node.right && stack.push(node.right);
        node && node.left && stack.push(node.left);
    }
    return arr
};
```


# N 叉树的层序遍历

```
var levelOrder = function(root) {
    if (!root) return [];
    let queue = [root];
    let ans = [];
    while(queue.length) {
        let level = [];
        let len = queue.length;
        for (let i = 0; i < len; i++) {
            let current = queue.shift();
            level.push(current.val);
            if (current.children && current.children.length > 0) {
                queue.push(...current.children);
            }
        }
        ans.push(level);
    }
    return ans;
};
```