树的面试题解法一般都是递归 -递归 Recursion
递归 - 循环
通过函数体来进行的循环
类似于栈的形式一层一层进去，栈本身就是递归调用时，系统给我们做的调用栈

递归 - 代码模板

function recur(level, param) { 
  // terminator 
  if (level > MAX_LEVEL) { 
    // process result 
    return; 
  }
  // process current logic 
  process(level, param); 
  // drill down 
  recur(level + 1, newParam); 
  // restore current status 
}



分治、回溯的实现和特性
分治 Divide & Conquer
分治和回溯是一种特殊的递归


分治代码模板

function divide_conquer(problem, param1, param2, ...) {
  # recursion terminator  递归终止条件
  if (!problem): 
    print_result 
    return 
  # prepare data 处理当前逻辑
  data = prepare_data(problem) 
  subproblems = split_problem(problem, data) 
  # conquer subproblems  下探到下一层
  subresult1 = divide_conquer(subproblems[0], p1, ...) 
  subresult2 = divide_conquer(subproblems[1], p1, ...) 
  subresult3 = divide_conquer(subproblems[2], p1, ...) 
  …
  # process and generate the final result 将最终结果合并
  result = process_result(subresult1, subresult2, subresult3, …)
    
  # revert the current level states 清理当前层
}