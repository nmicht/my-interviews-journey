# Algorithm exercises

1. Format a string as phone number in groups of three or two, but not less. The string can have other characters that are not numbers.  
Example:  
```
12---34-5-67 -> 123-45-67
-1-   2-3-4-5-6 -> 123-456
```

2. Build a hit  counter  
I do not remember all the details, but the requirements were changing during the call.
```js
class HitCounter {
    constructor() {
        this.hits = [] // array with timestamps
        this.hits = {
            
        }
        this.lastAccess;
    }
    
    counter(current = Date.now()) {
        this.clean(current)
        return this.hits.length
    }
    
    filter(current = Date.now()) {
        // return array of hits in the last five minutes
        let filterMins = 5 * 1000 * 60;
        return this.hits.filter((h) => h >= current - filterMins)
    }
    
    hit(current = Date.now()) {
        console.log(current.getMinutes())
        this.clean(current)
        let slots = 5 * 1000 * 60;
        min = current % slots
        // get the current minute // 3
        // if the key exists, increase
        // else create the key with 1 190319 16:18
        if (this.hits[min]) {
            this.hits.min ++
        } else {
            this.hits[min] = 1
        }
        this.hits.push(current) 
    }
    
    clean(current = Date.now()) {
        this.lastAccess = current
        // if my current and lastaccess are on the same range do nothing
        // else cleanup the hits dict
        this.hits = this.filter(current)
    }
} 


myHitCounter = new HitCounter()
myHitCounter.hit(0)
myHitCounter.hit(1000)
console.log(myHitCounter.hits)
console.log(myHitCounter.counter(5 * 1000 * 60 + 1)) // one
```
3. Build a shorten url service
4. Build a json comparison tool  
https://gist.github.com/emorikawa/07efb3213329b3272c0b2b247aa41ef7
4. Write the required code to make the tests runs without errors
```js
const assertEquals = ((i = 1) => (result, expected) =>
  console.log(`Assertion#${i++}: ${
    result === expected
      ? 'Passed'
      : `FAILED! expected ${result} to equal ${expected}`
    }`))();

// Set implementation ////////////////
class MySet {
    constructor(elements = []) {
        this.elements = []
        elements.forEach((el) => {
            this.add(el)
        })
    }
    
    add(element) {
        if(!this.has(element)) {
            this.elements.push(element)    
        }
    }
    
    get size() {
        return this.elements.length;
    }
    
    has(needle) {
        return !!this.elements.find((el) => el === needle)
    }
    
    union(otherSet) {
        return new MySet([...this.elements, ...otherSet.elements])
    }
    
    difference(otherSet) {
        return new MySet(this.elements.filter((el) => !otherSet.has(el)))
    }
}

// Tests ////////////////

console.log('Test 1')
const set1 = new MySet();
assertEquals(set1.size, 0);

console.log('Test 2')
const set2 = new MySet();
set2.add('a');
assertEquals(set2.size, 1);

console.log('Test 3');
const set3 = new MySet();
set3.add(1);
assertEquals(set3.has(1), true);
assertEquals(set3.has(2), false);

console.log('Test 4')
const set4 = new MySet([1,2,3]);
assertEquals(set4.size, 3);
assertEquals(set4.has(1), true);
assertEquals(set4.has(2), true);
assertEquals(set4.has(3), true);

console.log('Test 6')
const set6 = new MySet();
set6.add(1);
set6.add(1);
assertEquals(set6.has(1), true);
assertEquals(set6.size, 1);


console.log('Test 7')
const set7 = new MySet([1,1]);
assertEquals(set7.size, 1);

console.log('Test 8')
const set5a = new MySet();
const set5b = new MySet();

set5a.add(1);
set5a.add(2);

set5b.add(2);
set5b.add(4);

const set5c = set5a.union(set5b);
assertEquals(set5c.has(1), true);
assertEquals(set5c.has(2), true);
assertEquals(set5c.has(3), false);
assertEquals(set5c.has(4), true);
assertEquals(set5a.size, 2);
assertEquals(set5b.size, 2);

// Test 9
const set9a = new MySet();
const set9b = new MySet();

set9a.add(1);
set9a.add(2);
set9a.add(3);

set9b.add(3);
set9b.add(4);
set9b.add(5);

const set9c = set9a.difference(set9b);
assertEquals(set9c.has(1), true);
assertEquals(set9c.has(2), true);
assertEquals(set9c.has(3), false);
assertEquals(set9c.has(4), false);
assertEquals(set9c.has(5), false);
assertEquals(set9a.size, 3);
assertEquals(set9b.size, 3);
```

6. Build a carrousel from scratch 
https://codepen.io/adregan/collab/bd46202a79f5d927793686f1b1746f80


# Take home assigments
1. API for TicTacToe AI using the rules from Wikipedia, deployed to production.
2. Kyles tournament