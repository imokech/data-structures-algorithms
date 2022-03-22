# Data Structures and Algorithms
<a href="https://open.vscode.dev/imokech/data-structures-algorithm" rel="nofollow">
<img src="https://camo.githubusercontent.com/d66cf7a1b4fda80d31cce7848ed86d6d23497a946f396587fd24679b9181e29d/68747470733a2f2f6f70656e2e7673636f64652e6465762f6261646765732f6f70656e2d696e2d7673636f64652e737667" alt="Open in Visual Studio Code" data-canonical-src="https://open.vscode.dev/badges/open-in-vscode.svg" style="max-width: 100%;"></a>

## 🏗️ Data Structures
I want to prepare a repo to show power of data structures and algorithms.
Data structures are very important components for computers and programming
languages. Along with data structures, it is also very important to know how to solve
a problem or find a solution using these data structures.

(it will be completed ...)

## languages 

language | Big O 
--- | --- 
Lookup | O(1)
Push* | O(1) 
Insert | O(n)
Delete | O(n)

Data Structure | Languages | Examples | Algorithm
--- | --- | --- | --- 
Arrays | Javascript, (PHP soon) | Not yet | Not yet
Stacks | - | Not yet | Not yet
Queues | - | Not yet | Not yet
Linked Lists | - | Not yet | Not yet
Trees | - | Not yet | Not yet
Tries | - | Not yet | Not yet
Graphs | - | Not yet | Not yet
hash Tables | - | Not yet | Not yet

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
### Other names
Dictionary, maps, hash maps, objects
