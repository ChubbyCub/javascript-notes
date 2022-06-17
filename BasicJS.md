# Some notes on JavaScript language

### Variable declaration:

`let` vs. `const` vs `var`

* Variables are created with `undefined` value - variable creation stage. To make a variable no longer `undefined`, we need to assign a value to it.
* If you declare a variable with the `var` keyword in a function, that variable will be available to the entire function scope. See the Scope section below for example.

~~~~
var declaration;
console.log(declaration); // undefined
declaration = "test";
console.log(declaration); // test
~~~~

### Scope

> "If the variable statement occurs inside a FunctionDeclaration, the variables are defined with function-local scope in that function."

~~~~
function getDate() {
    var date = new Date();
    
    function formatDate() {
        return date.toDateString().slice(4); // date is defined here
    }
    
    return formatDate();
}

console.log(date); // ReferenceError

function discountPrices(prices, discount) {
    var discounted = [];
    
    for (var i = 0; i < prices.length; i++) {
        var discountPrice = prices[i] * (1 - discount);
        var finalPrice = Math.round(discountedPrice * 100) / 100;
        discounted.push(finalPrice);
    }
    
    console.log(i); // 3
    console.log(discountedPrice); // 150
    console.log(finalPrice); // 150
    return discounted;
}
~~~~

### Hoisting

When JS interpreter will assign variable declarations a default value of undefined during the `Creation` phase.

For example, if you write code like this: 

~~~~
function discountPrices(prices, discount) {
    var discounted = [];
    
    for (var i = 0; i < prices.length; i++) {
        var discountPrice = prices[i] * (1 - discount);
        var finalPrice = Math.round(discountedPrice * 100) / 100;
        discounted.push(finalPrice);
    }
    
    console.log(i); // 3
    console.log(discountedPrice); // 150
    console.log(finalPrice); // 150
    return discounted;
}
~~~~

This is what JS interprets:

~~~~
function discountPrices(prices, discount) {
    var discounted = undefined;
    var discountPrice = undefined;
    var finalPrice = undefined;
    
    discounted = []
    
    for (var i = 0; i < prices.length; i++) {
        discountPrice = prices[i] * (1 - discount);
        finalPrice = Math.round(discountedPrice * 100) / 100;
        discounted.push(finalPrice);
    }
    
    console.log(i); // 3
    console.log(discountedPrice); // 150
    console.log(finalPrice); // 150
    return discounted;
}
~~~~

Remember: 
* JS will hoist all your variables with `var` keyword to the top of the function scope.
* If you don't declare a variable with `var`/`const`/`let` keyword, that variable will belong to the global scope and will be accessible by any functions that shared that global scope.


