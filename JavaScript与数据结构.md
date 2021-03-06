# JavaScript与数据结构

## 一、数组

## 二、栈与队列

### 1、栈（后进先出LIFO）

#### 			1.1 栈的封装


```javascript
	// method: 方法 一般是和某一个对象实例有联系
	// function:  函数
	// 封装栈类
	function Stack() {
		this.items = []
		// 相关操作
		// 1.将元素加入到栈
		Stack.prototype.push = function (element) {
			this.items.push(element)
		}
		// 2.取出元素
		Stack.prototype.pop = function () {
			return this.items.pop()
		}
		// 3.查看栈顶元素
		Stack.prototype.peek = function () {
			return this.items[this.items.length - 1]
		}
		// 4.查看栈是否为空
		Stack.prototype.isEmpty = function () {
			return this.items.length == 0
		}
		// 5.获取栈中元素的个数
		Stack.prototype.size = function () {
			return this.items.length
		}
		// 6.toString方法
		Stack .prototype.toString = function () {
			let resultString = ''
			for (let i = 0; i < this.items.length; i++) {
				resultString += this.items[i]+' '
			}
			return resultString
		}
	}
```



```javascript
	// 使用栈
	let s= new Stack()
	s.push(10)
	s.push(20)
	s.push(30)
	console.log("栈顶元素"+s.peek())
	console.log("是否为空"+s.isEmpty())
	console.log("栈元素个数"+s.size())
	console.log("输出栈"+s.toString())
	</script>
```

#### 1.2 栈的应用之进制转换

```javascript
function Fun(i) {
			let s= new Stack()
			while(i > 0) {
				let a = i%2;
				 s.push(a)
				i = Math.floor(i/2)
			}
			// 因为顺序是倒过来的,重新遍历出来
			let list = ''
			while(!s.isEmpty()) {
				list += s.pop()+' '
			}
			return list
		}
```

### 2、队列(先进先出)

#### 	2.1 队列的封装

```javascript
<script>
	// 封装队列类
		function Queue() {
			this.items = []
			// 1.将元素加入队列
			Queue.prototype.enqueue() = function(element) {
				this.items.push(element)
			}
			// 2.删除队列中最前端的元素
			Queue.prototype.dequeue() = function() {
				return this.items.shift()
			}
			// 3.查看队列最前端的元素
			Queue.prototype.front() = function() {
				return this.items[0]
			}
			// 查看队列是否为空
			Queue.prototype.isEmpty() = function() {
				return this.items.length == 0
			}
			// 查看队列的元素个数
			Queue.prototype.size() = function() {
				return this.items.length
			}
			// toString方法
			Queue.prototype.toString() = function() {
				let resultString = ''
				for (let i = 0; i < this.items.length; i++) {
					resultString += [i] + ' '
				}
				return resultString
			}
		}
	</script>
```

#### 2.2 队列的应用之击鼓传花

```js
// 击鼓传花
			function passGame(nameList, num) {
				let queue = new Queue()
				for (var i = 0; i < nameList.length; i++) {
					queue.enqueue(nameList[i])
				}
				// 不是num加入会queue
				while(queue.size() >1) {
					for(let i = 0; i < num - 1; i++) {
						queue.enqueue(queue.dequeue())
					}
					queue.dequeue()
				}
				alert(queue.size())
				alert("最后剩下"+ queue.front())
			}
			names = ['n1','n2','n3','n4','n5']
			alert(passGame(names, 3))
```

#### 2.3 优先级队列

```js
<!--    封装优先级队列-->
    function PriorityQueue() {
      function QueueElement(element, priority) {
        this.element = element
        this.priority = priority
      }
      this.items = []
      /*
      * 两种情况：
      * 1.当队列中是空，那么就无需考虑优先级直接放进去就行了，
      * 2.当队列中已经有元素时候，进行比较，插入到比他大的元素（优先级值越小，优先级越大）,如果都没有插入，那么就是插入到最后一行
      *  */
      PriorityQueue.prototype.enqueue = function (element, priority) {
        let queueElement = new QueueElement(element, priority)
          if(this.items.length === 0) {
            this.items.push(queueElement)
          } else {
            let added = false
            for (let i = 0; i < this.items.length; i++) {
              if(queueElement.priority < this.items[i].priority) {
                this.items.splice(i, 0, queueElement)
                added = true
                break
              }
            }
            if(!added) {
              this.items.push(queueElement)
            }
          }
      }
      // 2.删除队列中最前端的元素
      PriorityQueue.prototype.dequeue = function() {
        return this.items.shift()
      }
      // 3.查看队列最前端的元素
      PriorityQueue.prototype.front = function() {
        return this.items[0]
      }
      // 查看队列是否为空
      PriorityQueue.prototype.isEmpty = function() {
        return this.items.length == 0
      }
      // 查看队列的元素个数
      PriorityQueue.prototype.size = function() {
        return this.items.length
      }
      // toString方法
      PriorityQueue.prototype.toString = function() {
        let resultString = ''
        for (let i = 0; i < this.items.length; i++) {
          resultString += this.items[i].element + '-'+this.items[i].priority+ '   '
        }
        return resultString
      }
    }
    let pq = new PriorityQueue()
    pq.enqueue('lin', 100)
    pq.enqueue('wu', 111)
    pq.enqueue('jin', 50)
    pq.enqueue('kan', 300)
    alert(pq)
```

## 三、链表

相对于数组来说：

​	1、链表的内存空间不是必须连续，可以充分考虑，灵活调动内存分配

​	2、链表在创建的时候不需要确定大小

​	3、链表在插入和删除数据的时候，时间复杂度可以达到O(1)。

​	4、访问时候会比数组效率低

#### 	3.1单向链表以及应用

#### 	3.2双向链表

![1645674271289.jpg](JavaScript与数据结构.assets/1645674271289.jpg.jpg)
