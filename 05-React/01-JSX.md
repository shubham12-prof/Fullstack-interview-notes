🔹 JSX (JavaScript XML)
JSX is a syntax extension for JavaScript that allows you to write HTML-like structure directly inside JavaScript.

Under the hood, Babel compiles JSX down to React.createElement() function calls, which return plain JavaScript objects called React elements.

JavaScript
// 1. What you write in JSX
const element = <h1 className="title">Hello World</h1>;

// 2. What it compiles to (Behind the scenes)
const compiledElement = React.createElement(
'h1',
{ className: 'title' },
'Hello World'
);
