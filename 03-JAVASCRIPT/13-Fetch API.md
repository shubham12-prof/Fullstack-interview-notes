13. Fetch API
    Q1: How do you use the Fetch API, and how do you handle HTTP errors properly?
    Answer:
    The fetch() method triggers a network request and returns a promise that resolves to a Response object.

Crucially, a fetch promise will not reject on HTTP error status codes (like 404 or 500). It only rejects on total network failures. You must manually verify the response.ok boolean property.

JavaScript
async function loadData() {
try {
const response = await fetch('[https://api.example.com/data](https://api.example.com/data)');

    // Code Explanation:
    // If response status is 404 or 500, response.ok is false. We throw to jump to catch block.
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    return data;

} catch (error) {
console.error("Fetch failed caught here:", error);
}
}
