14. Debounce
    Q1: What is Debouncing, and when should you use it?
    Answer:
    Debouncing delays the execution of a function until a specific amount of idle time has passed since the last time the event fired. It bunches multiple rapid, consecutive triggers into a single final execution.

Use case: Input search boxes. Waiting for a user to finish typing completely before sending an autocomplete API request, saving server processing power.

JavaScript
function debounce(func, delay) {
let timer;
return function(...args) {
// Code Explanation:
// Every single keystroke clears the previous timer, resetting the countdown clock
clearTimeout(timer);
timer = setTimeout(() => func.apply(this, args), delay);
};
}
