# Data Structures and Algorithms

## 🏗️ Data Structures
I want to prepare a repo to show power of data structures and algorithms.
Data structures are very important components for computers and programming
languages. Along with data structures, it is also very important to know how to solve
a problem or find a solution using these data structures.

(it will be completed ...)

## Table of Progress

Data Structure | Languages | Examples | Algorithm
--- | --- | --- | --- 
Arrays | Javascript | ✔ | Not yet
Stacks | Javascript, PHP | Not yet | Not yet
Queues | - | Not yet | Not yet
Linked Lists | Javascript, PHP | ✔ | reverse
Trees | - | Not yet | Not yet
Tries | - | Not yet | Not yet
Graphs | - | Not yet | Not yet
Hash Tables | Javascript | ✔ | Not yet

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
Type | Source 
--- | --- 
Array Vs Linked List | https://www.youtube.com/watch?v=DyG9S9nAlUM
Visual LinkedList | https://visualgo.net/en/list?slide=1

<br>
<br>

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

## Stack

<img src="https://raw.githubusercontent.com/imokech/data-structures-algorithm/main/assets/img/stack.png">

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