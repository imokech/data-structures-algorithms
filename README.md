# Data Structures and Algorithms

## 🏗️ Data Structures
I want to prepare a repo to show power of data structures and algorithms.
Data structures are very important components for computers and programming
languages. Along with data structures, it is also very important to know how to solve
a problem or find a solution using these data structures.

## Table of Progress

Data Structure | Languages | Examples 
--- | --- | --- 
Arrays | Javascript | ✔ 
Stacks | Javascript, PHP | ✔ 
Queues | Javascript, PHP | ✔ 
Linked Lists | Javascript, PHP | ✔ 
Trees | Javascript, PHP | ✔ 
Graphs | Javascript | ✔
Hash Tables | Javascript | ✔ 


## Table of Contents
  1. [Array](#array)
  2. [Hash Tables](#hash-tables)
  3. [Linked List](#linked-list)
  4. [Stack](#stack)
  5. [Queue](#queue)
  6. [Tree](#tree)
  7. [Graphs](#graph)


## Array

Action | Big O 
--- | --- 
Lookup | O(1)
Push* | O(1) 
Insert | O(n)
Delete | O(n)

`*` in dynamic array it can be O(n)

### Array Implementation in Javascript

``` JAVASCRIPT
let someArray = ['a', 'b', 'c', 'd', 'e'];

// Push - appending 'f' to the end of the array
someArray.push('f'); // O(1)

// Pop - removing last item of the array => 'f'
someArray.pop(); // O(1)

// Unshift - adding new element to the beginning of the array.
someArray.unshift('z'); // O(n)

// Remove - removing an item of the array
for( var i = 0; i < someArray.length; i++){  // O(n)
    if ( someArray[i] === 'd') { 
        someArray.splice(i, 1); 
    }
}
```
<br>
<br>


**[⬆ back to top](#table-of-contents)**
## Hash Tables
<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/hash_collision.png" alt="imokech - Hash Table">

A hash table is a data structure that implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found. (<a href="https://en.wikipedia.org/wiki/Hash_table">Wikipedia</a>)

### other names
- Javascript: object, map, set
- Ruby: hash
- Java: map
- Python: dictionary
- ...

Action | Big O 
--- | --- 
Insert | O(n)
Lookup* | O(1)
Delete | O(n)
Search | O(1) 

`*` depends on the hash funciton, it might take `O(n)`

One thing to keep in mind is Collision.
when you have a collision it slows down reading and writing with a hash table with `O(n/k)` (k is the size of your hash table) and we remove constants and simplify things it becomes an `O(n)`

<br>

### Hash Table Implementation in Javascript

``` JAVASCRIPT
let user = {
    age: 23,
    name: 'Mike',
    family: 'Specter',
    active: true,
    tellYourAge:  function () {
        console.log('My age is :' + this.age);
    }
}

user.age // O(1)
user.city = 'Oslo'; // O(1)
user.tellYourAge(); // O(1)

class HashTable {
constructor (size) {
    this.data = new Array(size)
}

// this is a private property
_hash(key) {
    let hash = 0;
    for (let i=0; i < key.length; i++) {
    // charCodeAt : represent utf-16 code (0 - 65535)
    hash = (hash + key.charCodeAt(i) * i) % this.data.length
    }

    return hash;
}

set(key, value) {
    let address = this._hash(key);

    if (!this.data[address]) {
    this.data[address] = [];
    }

    this.data[address].push([key, value]);

    return this.data
}

get(key) {
    let address = this._hash(key);
    const currentBucket = this.data[address];

    if (currentBucket.length) {
    for (let i = 0; i , currentBucket.length; i++) 
    {
        if (currentBucket[i][0] === key) {
            return currentBucket[i][1];
        } 
    }
    }

    return undefined;
}

keys() {
    const keysArray = [];
    
    for (let i=0; i < this.data.length; i++) {
    if (this.data[i]) {
        keysArray.push(this.data[i][0][0])
    }
    }

    return keysArray;
}
}

const myHash = new HashTable(100);
console.log(myHash._hash('fruits'))
console.log(myHash.set('cucomber', 8000))
console.log(myHash.set('apple', 5400))
console.log(myHash.set('peach', 2572))
console.log(myHash.get('peach'))

```
<br>
<br>

**[⬆ back to top](#table-of-contents)**
## Linked List
A linked list is a linear data structure, in which the elements are not stored at contiguous memory locations. The elements in a linked list are linked using pointers as shown in the below image:
<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/linked-list.png" alt="imokech - linked list" width="80%">

Action | Big O 
--- | --- 
Prepend | O(1)
Append | O(1)
Insert | O(n)
Lookup | O(n) 
Delete | O(n) 

### Linked List Implementation in Javascript
``` JAVASCRIPT
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    this.head = {
      value: value,
      next: null,
    }
    this.tail = this.head;
    this.length = 1;
  }

  append(value) {
    const newNode = new Node(value);

    this.tail.next = newNode;
    this.tail = newNode;
    this.length++;

    return this; // references this class instanciate
  }

  prepend(value) {
    const newNode = new Node(value);

    newNode.next =  this.head;
    this.head = newNode;
    this.length++;

    return this;
  }

  printList() {
    const array = [];
    let currentNode = this.head;
    while(currentNode !== null){
        array.push(currentNode.value)
        currentNode = currentNode.next
    }
    return array;
  }

  insert(index, value) {
    if (index >= this.length) {
      return this.append(value);
    }

    const newNode = new Node(value);
    const leader = this.traverseToIndex(index-1);
    const holdingPointer = leader.next;
    leader.next = newNode;
    newNode.next = holdingPointer;
    this.length++;

    return this.printList();
  }

  traverseToIndex(index) {
    let counter = 0;
    let currentNode = this.head;
    
    while(counter !== index) {
      currentNode = currentNode.next;
      counter++;
    }
    
    return currentNode;
  }

  remove(index) {
    const leader = this.traverseToIndex(index - 1);
    const unwantedNode = leader.next;
    leader.next = unwantedNode.next;
    this.length--;
    return this.printList();
  }

  reverse() {
    if (!this.head.next) {
      return this.head;
    }
    let first = this.head;
    let second = first.next;
   
    while(second) {
      const temp = second.next;
      second.next = first;
      first = second;
      second = temp;
    }
    this.head.next = null;
    this.head = first;
    
    return this;
  }
}

const mylinkedlist = new LinkedList(10);
mylinkedlist.append(5);
mylinkedlist.append(15);
mylinkedlist.prepend(1);
mylinkedlist.insert(1, 1000);
mylinkedlist.insert(3, 5000);
console.log(mylinkedlist.printList());
mylinkedlist.reverse();
console.log(mylinkedlist.printList());
```
### Linked List Implementation in PHP
``` PHP

class Node {
  public $data;
  public $next;
}

class LinkedList {
    public $head;

    public function __construct()
    {
        $this->head = null;
    }
  
    public function insert($value, $position)
    {     
        $newNode = new Node(); 
        $newNode->data = $value;
        $newNode->next = null;

        if($position < 1) {
            echo "\nposition should be >= 1.";
            return;
        }

        if ($position == 1) {
            $newNode->next = $this->head;
            $this->head = $newNode;
        } else {
            $temp = new Node();
            $temp = $this->head;
            for($i = 1; $i < $position-1; $i++) {
                if($temp != null) {
                    $temp = $temp->next;
                }
            }

            if (is_null($temp)) {
                echo "\nThe previous node is null.";
                return;
            }
            $newNode->next = $temp->next;
            $temp->next = $newNode;  
        }
    }  

    public function pop()
    {
        if(is_null($this->head)) {
            return null;
        }

        $temp = $this->head;
        $this->head = $this->head->next;
        $temp = null;  
    }

    public function prepend($value)
    {
        $newNode = new Node();
        $newNode->data = $value;
        $newNode->next = $this->head; 
        $this->head = $newNode;   
    }

    // Push
    public function append($value)
    {
        $newNode = new Node(); 
        $newNode->data = $value;
        $newNode->next = null;
        $this->head = $newNode;

        if(!is_null($this->head)) {
        $temp = new Node();
        $temp = $this->head;

        while($temp->next != null) {
            $temp = $temp->next;
        }

        $temp->next = $newNode;
        }    
    }

    public function remove($position)
    {     
        if($position < 1) {
        echo "\nposition should be >= 1.";
        return;
        }
        
        if ($position === 1 && !is_null($this->head)) {
            $nodeToDelete = $this->head;
            $this->head   = $this->head->next;
            $nodeToDelete = null;
        } else {
            $temp = new Node();
            $temp = $this->head;

            for($i = 1; $i < $position-1; $i++) {
                if($temp != null) {
                    $temp = $temp->next;
                }
            }

            if (is_null($temp) || is_null($temp->next)){
                echo "\nThe node is already null.";
                return;
            }

            $nodeToDelete = $temp->next;
            $temp->next = $temp->next->next;
            $nodeToDelete = null; 
        }
    } 

    public function find($value)
    {
        $temp = new Node();
        $temp = $this->head;
        $found = 0;
        $i = 0;

        if (is_null($temp)){
            echo "The list is empty.\n";
            return;
        }

        while(!is_null($temp)) {
            $i++;
            if($temp->data == $value) {
                $found++;
                break;
            }
            $temp = $temp->next;
        }

        if ($found == 1) {
            echo $value." is found at index = ".$i.".\n";
        } else {
            echo $value." is not found in the list.\n";
        }
    }
    
    public function reverseList()
    {
        if(is_null($this->head)) {
            return null;
        }

        $prevNode = $this->head;
        $tempNode = $this->head;
        $currentNode = $this->head->next;
        
        $prevNode->next = null;
        
        while($currentNode != null) {
            $tempNode = $currentNode->next;
            $currentNode->next = $prevNode;
            $prevNode = $currentNode;
            $currentNode = $tempNode;
        }

        $this->head = $prevNode;
    }   

    public function printList()
    {
        $temp = new Node();
        $temp = $this->head;
        if(is_null($temp)  {
            echo "The list is empty.\n";
            return;
        }

        echo "The list contains: ";
        while($temp != null) {
            echo $temp->data." ";
            $temp = $temp->next;
        }
        echo "\n";
    }   
};

$myLinkedList = new LinkedList();

$myLinkedList->append(10);
$myLinkedList->append(20);
$myLinkedList->append(30);
$myLinkedList->printList();

$myLinkedList->remove(2);
$myLinkedList->printList();

$myLinkedList->remove(1);
$myLinkedList->printList();  

/* 
 *  Other example with SplDoublyLinkedList
 **/
$linkedList = new SplDoublyLinkedList();

$linkedList->push('a');
$linkedList->push('b');
$linkedList->push('c');
$linkedList->push('d');

// FIFO : First In First Out => IT_MODE_FIFO
// LIFO : Last In First Out  => IT_MODE_LIFO
$linkedList->setIterationMode(SplDoublyLinkedList::IT_MODE_FIFO);
for ($linkedList->rewind(); $linkedList->valid(); $linkedList->next()) {
    echo $list->current()."\n";
    echo $list->key()."\n";
}
// Insert
$linkedList->add(0, 'x'); // O(n)
// Append
$linkedList->push('e'); // O(1)
// Prepend
$linkedList->unshift('e'); // O(1)
// Delete
unset($linkedList[0]); // O(n)

```
<br>

More information (for the curious!)
 Title  | Source 
--- | --- 
Array Vs Linked List | <a href="https://www.youtube.com/watch?v=DyG9S9nAlUM">Array Vs Linked List</a>
Visual LinkedList | <a href="https://visualgo.net/en/list?slide=1">Visual LinkedList</a>

<br>
<br>

**[⬆ back to top](#table-of-contents)**
## Doubly Linked List
<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/doubly_linked_list.gif">

### Doubly Linked List Implementation in Javascript
``` JAVASCRIPT
class DoublyNode {
  constructor(value) {
    this.value = value;
    this.next = null;
    this.prev = null;
  }
}

class DoublyLinkedList {
  constructor(value) {
    this.head = {
      value: value,
      next: null,
      prev: null
    }
    this.tail = this.head;
    this.length = 1;
  }

  append(value) {
    const newNode = new DoublyNode(value);

    newNode.prev = this.tail;
    this.tail.next = newNode;
    this.tail = newNode;
    this.length++;

    return this; // references this class instanciate
  }

  prepend(value) {
    const newNode = new DoublyNode(value);

    newNode.next =  this.head;
    this.head.prev = newNode;
    this.head = newNode;
    this.length++;

    return this;
  }

  printList() {
    const array = [];
    let currentNode = this.head;
    while(currentNode !== null){
        array.push(currentNode.value)
        currentNode = currentNode.next
    }
    return array;
  }

  insert(index, value) {
    if (index >= this.length) {
      return this.append(value);
    }

    const newNode = new DoublyNode(value);

    const leader  = this.traverseToIndex(index-1);
    const follwer = leader.next;
    leader.next  = newNode;
    newNode.prev = leader;
    newNode.next = follwer;
    follwer.prev = newNode;
    this.length++;

    return this.printList();
  }

  traverseToIndex(index) {
    let counter = 0;
    let currentNode = this.head;
    
    while(counter !== index) {
      currentNode = currentNode.next;
      counter++;
    }
    
    return currentNode;
  }

  remove(index) {
    const leader = this.traverseToIndex(index - 1);
    const unwantedNode = leader.next;
    leader.next = unwantedNode.next;
    this.length--;
    return this.printList();
  }

}

const myDoublyLinkedList = new DoublyLinkedList(10);
myDoublyLinkedList.append(5);
myDoublyLinkedList.append(15);
myDoublyLinkedList.prepend(1);
console.log(myDoublyLinkedList);
myDoublyLinkedList.insert(1, 1000);
myDoublyLinkedList.insert(3, 5000);
myDoublyLinkedList.insert(1);
```

**[⬆ back to top](#table-of-contents)**
## Stack

<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/stack.png" width="60%">

Action | Big O 
--- | --- 
Lookup | O(n)
Pop | O(1) 
Push | O(1)
Peek | O1n)

A stack is a linear data structure that follows the principle of Last In First Out (LIFO). This means the last element inserted inside the stack is removed first.

### Stack Implementation in Javascript

``` JAVASCRIPT
/**
 * Stacks (with Linked List)
 */

class Node {
  constructor(value){
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.top = null;
    this.bottom = null;
    this.length = 0;
  }

  peek() {
    return this.top;
  }

  push(value) {
    const newNode = new Node(value);

    if (this.length === 0) {
      this.top = newNode;
      this.bottom = newNode;
    } else {
      const holdingPointer = this.top;
      this.top = newNode;
      this.top.next = holdingPointer;
    }
    this.length++;
    return this;
  }

  pop() {
    if (!this.top) {
      return null;
    }
    if (this.top === this.bottom) {
      this.bottom = null;
    }

    const hlodingPointer = this.top;
    this.top = this.top.next;
    this.length--;
    return hlodingPointer;
  }
}

const myStack = new Stack();
console.log(myStack.push('stackoverflow'));
console.log(myStack.push('udemy'));
console.log(myStack.peek()); // udemy
console.log(myStack.pop());


/**
 * Stack (with Array)
 */
class Stack {
  constructor() {
    this.array = [];
  }

  peek() {
    return this.array[this.array.length - 1];
  }

  push(value) {
    this.array.push(value);
    return this;
  }

  pop() {
    this.array.pop();
    return this;
  }
}

const myStack = new Stack();
console.log(myStack.push('google'));
console.log(myStack.push('facebook'));
console.log(myStack.push('twitter'));
console.log(myStack.peek());
```

### Stack Implementation in PHP
``` PHP
class Stack 
{
    protected $stack;
    protected $size;

    public function __construct($size)
    {
        $this->stack = array();
        $this->size = $size;
    }

    public function push($item)
    {
        if (count($this->stack) < $this->size) {
            return array_unshift($this->stack, $item);
        } else {
            throw new RuntimeException('Stack is Full (overflow)');
        }
    }

    public function pop()
    {
        if(empty($this->stack)) {
            return new RuntimeException('Stack is Empty');
        } else {
            return array_shift($this->stack);
        }
    }

    public function peek()
    {
        return current($this->stack);
    }
}

$myBrowserHistory = new Stack(3);
var_dump($myBrowserHistory->push('google.com'));
var_dump($myBrowserHistory->push('twitter.com'));
var_dump($myBrowserHistory->peek()); // twitter.com
var_dump($myBrowserHistory->pop());

```
More information (for the curious!)
 Title  | Source 
--- | --- 
Visual Stack | <a href="https://visualgo.net/en/list?mode=Stack">Visual Stack</a>
Stack Data Structure | <a href="https://www.programiz.com/dsa/stack">Programiz</a>

<br>
<br>

**[⬆ back to top](#table-of-contents)**
## Queue
<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/queue.png">

Action | Big O 
--- | --- 
Lookup | O(n)
Enqueue | O(1) 
Dequeue | O(1)
Peek | O1n)

Queue follows the First In First Out (FIFO) rule - the item that goes in first is the item that comes out first.
In the above image, since 1 was kept in the queue before 2, it is the first to be removed from the queue as well. It follows the FIFO rule.

### Stack Implementation in Javascript

``` JAVASCRIPT
class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.length = 0;
  }

  peek() {
    return this.first;
  }

  enqueue(value) {
    const newNode = new Node(value);
    if(this.length === 0) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    this.length++;
    return this;
  }

  dequeue() {
    if (!this.first){
      return null;
    }
    if (this.first === this.last) {
      this.last = null;
    }
    const hlodingPointer = this.first;
    this.first = this.first.next;
    this.length--;
    return hlodingPointer;
  }
}

const myQueue = new Queue();
console.log(myQueue.enqueue('first person'));
console.log(myQueue.enqueue('second person'));
console.log(myQueue.enqueue('third person'));
console.log(myQueue.peek()); // first person
console.log(myQueue.dequeue());
```

### Stack Implementation in PHP

``` PHP
class Queue 
{
    protected $queue;

    public function __construct()
    {
        $this->queue = array();
    }

    public function enqueue($item)
    {
        array_push($this->queue, $item);
        return $this->queue;
    }

    public function dequeue()
    {
        if(empty($this->queue)) {
            return new RuntimeException('There is no Queue');
        } else {
            return array_shift($this->queue);
        }
    }

    public function peek()
    {
        // Queue is ordered list, so we can use 0 index to get first input
        return $this->queue[0] ?? null;
    }
}

$restaurantQueue = new Queue();
var_dump($restaurantQueue->enqueue('first person'));
var_dump($restaurantQueue->enqueue('second person'));
var_dump($restaurantQueue->enqueue('third person'));
var_dump($restaurantQueue->peek()); // first person
var_dump($restaurantQueue->dequeue());
```

More information (for the curious!)
 Title  | Source 
--- | --- 
Visual Queue | <a href="https://visualgo.net/en/list?mode=Queue">Visual Queue</a>
Queue Data Structure | <a href="https://www.programiz.com/dsa/queue">Programiz</a>

<br>
<br>

**[⬆ back to top](#table-of-contents)**
## Tree
<p float="left">
  <img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/nodes-edges.png" width="49%">
  <img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/height-depth.png" width="39%">
</p>

A tree whose elements have at most 2 children is called a binary tree. Since each element in a binary tree can have only 2 children, we typically name them the left and right child. Trees are a special Abstract Data Type (ADT) that
represents hierarchical data.


Other Data Structures of Tree 
 Name  | Completed
--- | --- 
Balanced vs Unbalanced | -
BST | ✔ 
BSH | -
AVL | ✔ 
Red Black | ✔ 
Trie | -

### Tree Implementation in PHP
``` PHP
// Implementation : Tylere Willis (tylerewillis.com)
class Node
{
    function __construct($data)
    {
        $this->data = $data;
        $this->parent = null;
        $this->children = array();
    }
}

class Tree
{
    public function __construct($data)
    {
        $node = new Node($data);
        $this->root = $node;
        $this->levels = 0;
    }

    public function add($data, $toParent)
    {
        $child = new Node($data);
        $parent = false;
        $results = $this->traverseBreadthFirst();

        foreach ($results as $result) {
            if ($result->data == $toParent) {

                // Add as child to node
                $result->children[] = $child;

                // Add node as child's parent
                $child->parent = $result->data;

                // Parent located so true
                $parent = true;
            }
        }

        if ($parent == false) {
            echo "Error: Cannot add node to non-existent parent.";
        }
    }

    public function remove($data, $fromParent) {
        $results = $this->traverseBreadthFirst();
        foreach($results as $result) {
            if($result->data == $fromParent) {
                $i = 0;
                foreach($result->children as $child) {
                    if($child->data == $data) {
                        unset($result->children[$i]);
                        break;
                    }
                    $i++;
                }
            }
        }
    }

    public function contains($data) {
        $results = $this->traverseBreadthFirst();
        foreach($results as $result) {
            if($result->data == $data) {
                return $result;
            }
        }
    }

    public function traverseDepthFirst() {
        function recurse($currentNode, &$results = array()) {
            $length = count($currentNode->children);
            for ($i = 0; $i < $length; $i++) {
                $results[] = $currentNode->children[$i];
                recurse($currentNode->children[$i], $results);
            }
        }
        recurse($this->root, $results);
        return $results;
    }
    
    // Breadth-first traversal
    public function traverseBreadthFirst() {
        $queue = array();
        $queueIndex = 1;
        $results = array();
    
        array_push($queue, $this->root);
        array_push($results, $this->root);
    
        $currentTree = $queue[0];
        unset($queue[0]);
    
        while($currentTree) {
            $length = count($currentTree->children);
            for ($i = 0; $i < $length; $i++) {
                array_push($queue, $currentTree->children[$i]);
                array_push($results, $currentTree->children[$i]);
            }
            if(count($queue) > 0) {
                $currentTree = $queue[$queueIndex];
                unset($queue[$queueIndex]);
            } else {
                $currentTree = false;
            }
            $queueIndex++;
        }
        return $results;
    }
}

$tree = new Tree(10);
var_dump($tree->add(5, 10));
var_dump($tree);
var_dump($tree->remove(5, 10));
var_dump($tree);

```
<br>

### Binary Search Tree
Action | Big O 
--- | --- 
Lookup | O(log N)
Insert | O(log N)
Delete |O(log N)


### Binary Search Tree Implementation in Javascript


``` JAVASCRIPT
class Node {
  constructor(value) {
    this.left = null; 
    this.right = null; 
    this.value = value; 
  }
}

class BinarySearchTree 
{
  constructor(){
    this.root = null;
  }
  
  insert(value) {
    const newNode = new Node(value);
    if (this.root == null) {
      this.root = newNode
    } else {
      let currentNode = this.root;
      while(true) {
        if (value < currentNode.value) {
          // Left
          if (!currentNode.left) {
            currentNode.left = newNode;
            return this;
          }
          currentNode = currentNode.left;
        } else {
          // Right
          if (!currentNode.right) {
            currentNode.right = newNode;
            return this;
          }
          currentNode = currentNode.right;
        }
      }
    }
  }

  lookup(value) {
    if (!this.root) {
      return false;
    }
    let currentNode = this.root;
    while(currentNode) {
      if (value < currentNode.value) {
        currentNode = currentNode.left;
      } else if (value > currentNode.value) {
        currentNode = currentNode.right;
      } else if (value === currentNode.value) {
        return currentNode;
      }
    }
    return false;
  }

  remove(value) {
    if(!this.root) {
      return false;
    }

    let currentNode = this.root;
    let parentNode = null;
    while(currentNode) {
      if (value < currentNode.value) {
        parentNode = currentNode;
        currentNode = currentNode.left;
      }else if (value > currentNode.value) {
        parentNode = currentNode;
        currentNode = currentNode.right;
      } else if (currentNode.value === value) {
        if (currentNode.right === null) {
          if (parentNode === null) {
            this.root = currentNode.left;
          } else {
            if (currentNode.value < parentNode.value) {
              parentNode.left = currentNode.left;
            } else if (currentNode.value > parentNode.value) {
              parentNode.right = currentNode.left;
            }
          }
        } else if (currentNode.right.left === null) {
          if (parentNode === null) {
            this.root = currentNode.left;
          } else {
            currentNode.right.left = currentNode.left;

            if (currentNode.value < parentNode.value) {
              parentNode.left = currentNode.right;
            } else if (currentNode.value > parentNode.value) {
              parentNode.right = currentNode.right;
            }
          }
        } else {
          let leftmost = currentNode.right.left;
          let leftmostParent = currentNode.right;
          while (leftmost.left !== null) {
            leftmostParent = leftmost;
            leftmost = leftmost.left;
          }

          leftmostParent.left = leftmost.right;
          leftmost.left = currentNode.left;
          leftmost.right = currentNode.right;

          if (parentNode === null) {
            this.root = leftmost;
          } else {
            if (currentNode.value < parentNode.value) {
              parentNode.left = leftmost;
            } else if (currentNode.value > parentNode.value) {
              parentNode.right = leftmost;
            }
          }
        }
        return true;
      }
    }
  }
}

const tree = new BinarySearchTree();

console.log(tree.insert(9));
console.log(tree.insert(8));
console.log(tree.insert(7));
console.log(tree.lookup(8));
console.log(tree.remove(7));

```


### AVL Tree
An AVL tree is a self-balancing binary search tree where the heights of two child
subtrees of a node will differ by a maximum of 1. If the height increases, in any case,
there will be a rebalance to make the height difference to 1. This gives the AVL tree
an added advantage of logarithmic complexity for different operations.

### Red-Black Tree
<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/Red-black_tree.svg" width="39%">

A red-black tree is a self-balanced binary search tree with some extra properties,
which is the color. Each node in the binary tree stores one extra bit of information,
which is known as color and can have either red or black as values. Like an AVL
tree, a red-black tree is also used for real-time applications as the average and worst
case complexity is also logarithmic.

More information (for the curious!)
 Title  | Source 
--- | --- 
Visual Tree | <a href="https://visualgo.net/en/bst?slide=1">Visual Tree</a>
Trees (Full) | <a href="https://www.geeksforgeeks.org/binary-tree-data-structure/">GeeksForGeeks</a>
Trees (Summary) | <a href="https://www.programiz.com/dsa/trees">Programiz</a>

**[⬆ back to top](#table-of-contents)**
## Graphs


<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithms/main/assets/img/graph-var.png" alt="imokech - Graph">
<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithms/main/assets/img/graph1.png" alt="imokech - Graph" width="50%">



A graph data structure consists of a finite (and possibly mutable) set of vertices (also called nodes or points), together with a set of unordered pairs of these vertices for an undirected graph or a set of ordered pairs for a directed graph.  (<a href="https://en.wikipedia.org/wiki/Graph_(abstract_data_type)">Wikipedia</a>)

<br>

### Graph Implementation in Javascript

``` JAVASCRIPT

class Graph {
  constructor() {
    this.numberOfNodes = 0;
    this.adjacentList = {};
  }
  addVertex(node) {
    this.adjacentList[node] = [];
    this.numberOfNodes++;
  }
  addEdge(node1, node2) {
    // undirected Graph
    this.adjacentList[node1].push(node2);
    this.adjacentList[node2].push(node1);
  }

  showConnections() {
    const allNodes = Object.keys(this.adjacentList);
    for (let node of allNodes) {
      let nodeConnections = this.adjacentList[node];
      let connections = "";
      let vertex;
      for (vertex of nodeConnections) {
        connections += vertex + " ";
      }
      console.log(node + " ---> " + connections)
    }
  }

}

const myGraph = new Graph();
myGraph.addVertex('0');
myGraph.addVertex('1');
myGraph.addVertex('2');
myGraph.addVertex('3');
myGraph.addVertex('4');
myGraph.addVertex('5');
myGraph.addVertex('6');
myGraph.addEdge('3', '1');
myGraph.addEdge('3', '4');
myGraph.addEdge('4', '2');
myGraph.addEdge('4', '5');
myGraph.addEdge('1', '2');
myGraph.addEdge('1', '0');
myGraph.addEdge('0', '2');
myGraph.addEdge('6', '5');

myGraph.showConnections();

```
<br>
<br>

**[⬆ back to top](#table-of-contents)**