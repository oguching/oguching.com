I've been reading [JavaScript Allongé](https://leanpub.com/javascript-allonge/read)
and came across this piece of code 

```JavaScript
  function K (x) {
      return function (y) { 
          return x
      }
  };
```

It's called a K Combinator. What does it do? Well K is a function that accepts an argument. If we call K 
with an argument, it returns a function. That is K(9) returns this `function (y) { return x }`. If we then
call K(9) with an argument like so `K(9)('bow wow')` it returns `9`. 

I was thinking of this and it reminds me of the scene in the Lord of the Rings where Gandalf give Frodo
the one ring and warns him to keep it secret, keep it safe. Then he leaves to find out more about the ring.

<iframe width="560" height="315" src="https://www.youtube.com/embed/_YhpauKGgQ4" frameborder="0" allowfullscreen></iframe>

Gandalf comes back to Frodo asking him for the ring and Frodo shows it to him. Basically the same thing happening here.
I pass something to K() and say here, keep it for me, then I come back to K() and and ask for the first thing I passed and
K() hands it to me. Of course the second call does not have to accept anything so we can modify it so that `K(9)()` returns `9`.
