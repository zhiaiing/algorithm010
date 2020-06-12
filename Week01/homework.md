# 删除排序数组中的重复项
    1.暴力破解法 --- 两层嵌套循环 --- 时间复杂度 O(n^2)
    2.快慢指针法 --- 时间复杂度 O(n)

```
    var removeDuplicates = function(nums) {
        const length = nums.length;
        if (nums === 0) return 0;
        var i = 0;
        for(j = 1; j <= length-1; j++) {
            if (nums[j] !== nums[i]) {
                nums[++i] = nums[j];
            } 
        }
        nums.splice(i+1,length - i);
    };
```



# 旋转数组
    1. 暴力枚举 --- 时间复杂度 O(n * k) 
    2. 单次反转法 --- 每次把最后一个元素插入到第一个元素位置 时间复杂度 O(k) 
    3. 中间反转数组 --- k%length --- 时间复杂度 O(1) 

```
    var rotate = function(nums, k) {
        nums.splice(0, 0, ...nums.splice(nums.length - k))
    };
```



# 合并两个有序链表
    1. 暴力递归 --- 时间复杂度 O((i + j)^2) 
    2. 双指针 --- 时间复杂度 O(i + j) 

```
    var mergeTwoLists = function(l1, l2) {
        let listNode = new ListNode(0), result = listNode;
        while(l1 && l2) {
            if (l1.val <= l2.val) {
                listNode.next = l1;
                l1 = l1.next;
            } else {
                listNode.next = l2;
                l2 = l2.next;
            }
            listNode = listNode.next;
        }
        listNode.next = l1 ? l1 : l2;
        return result.next;
    };
```



# 合并两个有序数组
    1. 暴力循环法 --- 时间复杂度 O(m*n) 
    2. 双指针法  --- 时间复杂度 O(m+n) 

```
    var merge = function(nums1, m, nums2, n) {
        let totleLength = m + n;
        while(n > 0) {
            if (m <=0) {//nums1原数据排完了空了, 后面直接排nums2的元素
                nums1[--totleLength] = nums2[--n];
            } else {
                nums1[--totleLength] = nums1[m-1] < nums2[n-1] ? nums2[--n] : nums1[--m]
            }
        }
    };
```



# 两数之和
    1. 暴力枚举 --- 两层嵌套循环 --- 时间复杂度 O(n^2)
    2. 缓存法 --- 单次循环(找不到缓存当前的值) --- 时间复杂度 O(n)

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



# 加一
    1. 使用栈+进位符 --- 时间复杂度 O(n)
    2. 反向遍历+进位符(在原数组上改) --- 时间复杂度 O(n)

```
    var plusOne = function(digits) {
        let rest = 1;
        for(let i = digits.length - 1; rest > 0 && i >= 0; i--) {
            const result = digits[i] + rest;
            result >= 10 ? (digits[i] = result%10, rest = 1) :  (digits[i] = result, rest = 0)
        }
        if (rest > 0) {
            digits.unshift(1);
        }
        return digits;
    };
```



# 设计循环双端队列

```
    /**
    * Initialize your data structure here. Set the size of the deque to be k.
    * @param {number} k
    */
    var MyCircularDeque = function(k) {
        this.length = k;
        this.stack = [];
    };

    /**
    * Adds an item at the front of Deque. Return true if the operation is successful. 
    * @param {number} value
    * @return {boolean}
    */
    MyCircularDeque.prototype.insertFront = function(value) {
        if (this.stack.length >= this.length) {
            return false;
        }
        this.stack.unshift(value);
        return true;
    };

    /**
    * Adds an item at the rear of Deque. Return true if the operation is successful. 
    * @param {number} value
    * @return {boolean}
    */
    MyCircularDeque.prototype.insertLast = function(value) {
        if (this.stack.length >= this.length) {
            return false;
        }
        this.stack.push(value);
        return true;
    };

    /**
    * Deletes an item from the front of Deque. Return true if the operation is successful.
    * @return {boolean}
    */
    MyCircularDeque.prototype.deleteFront = function() {
        if (this.stack.length === 0) return false;
        this.stack.shift();
        return true;
    };

    /**
    * Deletes an item from the rear of Deque. Return true if the operation is successful.
    * @return {boolean}
    */
    MyCircularDeque.prototype.deleteLast = function() {
        if (this.stack.length === 0) return false;
        this.stack.pop();
        return true;
    };

    /**
    * Get the front item from the deque.
    * @return {number}
    */
    MyCircularDeque.prototype.getFront = function() {
        if (this.stack.length === 0) return -1;
        return this.stack[0];
    };

    /**
    * Get the last item from the deque.
    * @return {number}
    */
    MyCircularDeque.prototype.getRear = function() {
        if (this.stack.length === 0) return -1;
        return this.stack[this.stack.length -1];
    };

    /**
    * Checks whether the circular deque is empty or not.
    * @return {boolean}
    */
    MyCircularDeque.prototype.isEmpty = function() {
        return this.stack.length === 0;
    };

    /**
    * Checks whether the circular deque is full or not.
    * @return {boolean}
    */
    MyCircularDeque.prototype.isFull = function() {
        return this.stack.length === this.length;
    };
```



# 接雨水
    1. 暴力循环 --- 双层循环 ---找到对应index的左右边界 --- 时间复杂度 O(n^2)
    2. 两次遍历，遍历出每个item的左右边界, 在遍历一次算出每个item可存的水量 --- 时间复杂度 O(n)
    3. 利用栈，一次遍历 --- 时间复杂度 O(n)
    4. 方法2优化版,双端夹逼 --- 找到对应index下相对的左右边界 --- 时间复杂度 O(n)
```
    方法2
    var trap = function(height) {
        if (height.length < 3) return 0;
        const length = height.length, leftArr = [height[0]], rightArr = [height[length - 1]];

        for(let i = 1; i < length; i++) {
            leftArr.push((Math.max(leftArr[leftArr.length -1], height[i])));
        }
        for(let j = length - 2; j >= 0; j--) {
            rightArr.push((Math.max(rightArr[rightArr.length -1], height[j])));
        }

        let area = 0;

        for(let k = 0; k < length; k++) {
            area += Math.min(leftArr[k], rightArr[length - k -1]) - height[k];
        }
        return area;
    };  

    方法3
    var trap = function(height) {
        if (height.length < 3) return 0;
        const stack = [0], length = height.length;
        let area = 0;
        for(let i = 1; i < length; i++) {
            while(height[stack[stack.length -1]] <= height[i]) {
                const lastVal = height[stack.pop()];
                if (stack.length === 0) {
                    break;
                }
                area += (Math.min(height[i], height[stack[stack.length - 1]]) - lastVal) * (i - stack[stack.length - 1] -1);
            }
            stack.push(i)
        }
        return area;
    };

    方法4
    var trap = function(height) {
        if (height.length < 3) return 0;
        let left = 0, right = height.length - 1, leftMaxValue = height[0], rightMaxValue = height[height.length - 1], area = 0; 

        while(left < right) {
            leftMaxValue < rightMaxValue ? (area += leftMaxValue - height[left++], leftMaxValue = Math.max(leftMaxValue, height[left])) : (area += rightMaxValue - height[right--], rightMaxValue = Math.max(rightMaxValue, height[right]));
        }

        return area;
    };
```