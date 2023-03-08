1. 快慢指针找环入口：
   设head到环入口的距离为a，快慢指针相遇的点距环入口距离为b，环的长度为L。
   **注**：快慢指针相遇时，慢指针所走的路程a+L。
   2*(a+b) = a+b+n*L  
   a = n*L - b  
   因此，fast此时再走a距离，即2a+b+n*L = a + 2n*L，也就是此时fast位于环入口处。  
   所有创建一个指针指向head，和fast一起往后走，他们相遇时即为环入口。

2. priority_queue优先队列：默认为大顶堆  
   小顶堆写法示例：priority_queue<int, vector<int>, greater<int>>。
   - push/pop(): o(log n) 
   - top(): o(1)
   - 第一个非叶结点下标：length / 2 - 1
   - 左孩子下标：2 * i + 1
   - 右孩子下标：2 * i + 2
   - 父亲下标：（i - 1）/ 2   
  将原有数组原地建大顶堆：从第一个非叶结点开始每个节点都做下沉，即与左右孩子比较、交换并递归做交换的结点。  
  取堆顶： 将堆顶与最后一个元素交换，然后下沉堆顶。  
  因此，将下沉操作写成函数如下：
  ``` c++
  void BuildMaxPile(vector<int>& nums, int i){//下沉
      int largest = i, left = i*2+1, right = left + 1;

      if(left < nums.size() && nums[left] > nums[largest]){
         largest = left;
      }

      if(right < nums.size() && nums[right] > nums[largest]){
         largest = right;
      }
      
      if(largest != i){//如果i是最大的，直接返回，否则交换nums[i]和最大的，并继续下沉
         swap(nums[i], nums[largest]);
         BuildMaxPile(nums, largest);
      }
      return;
   }
   ``` 
3. 单调栈：栈内元素或以元素为下标的值单调递增或递减，即入栈操作不破坏栈的单调性。用于解决找最近一个比当前元素大或小的元素。
