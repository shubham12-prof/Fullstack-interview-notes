15. Throttle
    Q1: What is Throttling, and how does it differ from Debouncing?
    Answer:
    While debouncing waits for a quiet pause in triggers, Throttling limits code execution to at most once every specific time interval. It guarantees regular, periodic running updates regardless of how many actions fire.

Use case: UI scroll listeners. Recalculating page layout alignments every 200ms while a user drops down a long article.
