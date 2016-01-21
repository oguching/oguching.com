I was preparing a post on looping in JavaScript but then came across this [post](http://developer.telerik.com/featured/the-javascript-looping-evolution/) by Cody Lindley so I'm not going to do that. 
Instead I'm going to talk about accessing the first and last elements in an array. Consider this code:

```JavaScript
  let numbers = ['one', 'two', 'three'];
  
  let first = numbers[0],
        len = numbers.length,  //3
       last = numbers[len - 1];
  
  console.log(first);    // logs "one"
  console.log(last);     // logs "three"     
       
```

So pretty simple, we assign the first element in the array to `first` and compute the last element from the length of the elements in the array
and assign it to `last`. Now let's add elements to the array and see if we can still access the first and last elements.

```JavaScript
  numbers.push('four', 'five');  // returns 5
  
  console.log(first);    // logs "one"
  console.log(last);     // logs "three"
  
```

It puzzled me that `last` does not log `"five"`, I expected it to always track the last element but it doesn't. Why? Remember <pre> last = numbers[len - 1]; </pre>
what we did there is assign `numbers[2]` which contains `"three"` at the time, to `last`. So `last` always contains that value. It seems so obvious but
I obviously didn't get it at first. How do we fix it? We do what [lodash](https://github.com/lodash/lodash) does, we write a function.

```JavaScript
  function last(array) {
    let length = array.length;
    return array[length - 1];
  }
  
  last(numbers);       // logs "five"
  
  numbers.push('six', 'seven');
  
  last(numbers);       // logs "seven"
  
  numbers[10] = 'ten';
  
  last(numbers);       // logs "ten"
  
```  

So this works. I'm so glad for the folks at [/r/javascript](https://www.reddit.com/r/javascript) for their help understanding this code. That's it, that's the post.