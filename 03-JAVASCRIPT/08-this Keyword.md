Q1: How is the value of the this keyword determined?
Answer:
The value of this is not static; it is determined dynamically based entirely on how a function is called:

Implicit Binding: When a function is called as an object method, this points to the object left of the dot (obj.method()).

Explicit Binding: call(), apply(), and bind() force this to point to a specific target object.

Arrow Functions: Arrow functions do not have their own this. They inherit this lexically from their surrounding outer block scope.

JavaScript
const user = {
name: "John",
greet: function() {
console.log(`Hello, ${this.name}`);
}
};

// Code Explanation:
user.greet(); // Logs "Hello, John" because user is to the left of the dot invocation
