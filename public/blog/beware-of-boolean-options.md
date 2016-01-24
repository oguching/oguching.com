I was reading about [Factory Pattern](https://carldanley.com/js-factory-pattern/) on Carl Danley's blog recently and ran the code that accompanied the
post on jsfiddle but didn't get same result as he did. We're going to explore why but first, I mentioned 
Factory Pattern. What is it? [Addy Osmani](https://twitter.com/addyosmani) wrote a book, *[JavaScript design patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)* and says the following about the Factory pattern:

> The Factory pattern is another creational pattern concerned with the notion of creating objects. Where it differs from the other patterns in its category is that it doesn't explicitly require us use a constructor. Instead, a Factory can provide a generic interface for creating objects, where we can specify the type of factory object we wish to be created.

You should check out the [book](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#factorypatternjavascript) if you haven't already but let's get on with our example:

```JavaScript
  function CarDoor( options ) {
   this.color = options.color || 'red';
   this.side = options.side || 'right';
   this.hasPowerWindows = options.hasPowerWindows || true;
  }

  function CarSeat( options ) {
    this.color = options.color || 'gray';
    this.material = options.material || 'leather';
    this.isReclinable = options.isReclinable || true;
  }

  function CarPartFactory() {}
    CarPartFactory.prototype.createPart = function createCarPart( options ) {
    var parentClass = null;
  
    if( options.partType === 'door' ) {
      parentClass = CarDoor;
    } else if( options.partType === 'seat' ) {
      parentClass = CarSeat;
    }
  
    if( parentClass === null ) {
      return false;
    }
  
    return new parentClass( options );
  }

  // example usage
  var myPartFactory = new CarPartFactory();
  var seat = myPartFactory.createPart( {
    partType : 'seat',
    material : 'leather',
    color : 'blue',
    isReclinable : false
  } );

  // outputs: true
  console.log( seat instanceof CarSeat );

  // outputs a CarSeat object with material "leather", color "blue", isReclinable "false"
  console.log( seat );
```
That's our code, you may have already spot the mistake but let's go through it. We have a `CarSeat()` function and a `CarDoor()` function with their respective properties. You will notice these functions have names that are capitalised, this is JavaScript convention for constructor functions. It means we will have to call `new` on them at some point. The `CarPartFactory()` function has a `createPart()` prototype function that checks the type of part we want and calls the respective constructor function.

We create a `myPartFactory` object from `CarPartFactory()` then use it to call `createPart()`, define the properties (`partType: 'seat', material: 'leather', color: 'blue', isReclinable: false`) and assign the value to `seat`. We then log seat to console and should get <pre>Object { color: "red", material: "cloth", isReclinable: false }</pre> but we don't. What's going on here? We assigned `isReclinable: false` yet we are getting back `true`. 

Let's look into our CarSeat() function and see what's happening there. We are using logical OR (`||`) to set default values, logical expressions are evaluated left to right. If no option is passed for the property, the value to the right of the `||` is used. However extra caution is required when dealing with Boolean values. The rule `true || (anything)` always evaluates to `true`, this is where the problem lies. When we pass in `false`, it's always evaluated as `true`.

We can fix it by removing the logical OR so that if isReclinable is not defined that value is simply `undefined`.

```JavaScript
  function CarSeat( options ) {
    this.color = options.color || 'gray';
    this.material = options.material || 'leather';
    this.isReclinable = options.isReclinable;
  }
```
A better option is to avoid the Boolean trap altogether, we can give
 `isReclinable` the options `reclinable` and `non-reclinable` instead of `true` and `false`.

There's a talk by Ariya Hidayat on [JavaScript API design principles](https://www.youtube.com/watch?v=HYl7ReNB5TA) that deals with these kinds of issues that's totally worth watching.