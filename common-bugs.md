# Loss of function context ```this```.

## Without solution
`this` currently references undefined
```js
  onDelete: function () {
    setTimeout(
      function () {
        this.model.destroy();
        this.remove();
      }
    );
  },
```
## Solution #1
The `bind()` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
```js
  onDelete: function () {
    setTimeout(
      function () {
        this.model.destroy();
        this.remove();
      }.bind(this) // <-- Add .bind(this)
    ); 
  },
```
## Solution #2
A common mistake is to extract a method from an object, then to later call that function and expect it to use the original object as its this (e.g., by using the method in callback-based code). Without special care, however, the original object is usually lost. Creating a bound function from the function, using the original object solves this problem.
```js
  onDelete: function () {
  var that = this;  // <-- Added code
  setTimeout(
    function () {
      that.model.destroy();  // <-- Added code
      that.remove();  // <-- Added code
    }
  );
}
```
