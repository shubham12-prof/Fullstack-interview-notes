Q1: Explain Prototype-based Inheritance and the Prototype Chain.
Answer:
Every JavaScript object contains an internal fallback link to another object called its Prototype (accessible via **proto**).

When you look up a property or method on an object, JavaScript checks the object itself first. If missing, it travels up the Prototype Chain to check the prototype object, continuing until it either finds the property or reaches null.

JavaScript
const animal = { eats: true };
const dog = Object.create(animal); // Links dog's prototype to animal

dog.barks = true;

// Code Explanation:
console.log(dog.barks); // true (found directly on the dog object)
console.log(dog.eats); // true (found by climbing up the prototype chain to 'animal')
