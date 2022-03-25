# Data Structures and Algorithms
<a href="https://open.vscode.dev/imokech/data-structures-algorithm" rel="nofollow">
<img src="https://camo.githubusercontent.com/d66cf7a1b4fda80d31cce7848ed86d6d23497a946f396587fd24679b9181e29d/68747470733a2f2f6f70656e2e7673636f64652e6465762f6261646765732f6f70656e2d696e2d7673636f64652e737667" alt="Open in Visual Studio Code" data-canonical-src="https://open.vscode.dev/badges/open-in-vscode.svg" style="max-width: 100%;"></a>

## 🏗️ Data Structures
I want to prepare a repo to show power of data structures and algorithms.
Data structures are very important components for computers and programming
languages. Along with data structures, it is also very important to know how to solve
a problem or find a solution using these data structures.

(it will be completed ...)

## Data Structures and languages

Data Structure | Languages | Examples | Algorithm
--- | --- | --- | --- 
Arrays | Javascript, (PHP soon) | ✔ | Not yet
Stacks | - | Not yet | Not yet
Queues | - | Not yet | Not yet
Linked Lists | - | Not yet | Not yet
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

### Array in Use (Javascript)

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
## Hash Tables
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

### Hash Table in Use (Javascript)

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
