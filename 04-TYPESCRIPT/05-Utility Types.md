4. Utility Types
   Q1: Explain common TypeScript Utility Types like Partial, Required, Readonly, and Pick.
   Answer:
   TypeScript provides built-in utility types to transform existing types into new variations:

Partial<T>: Constructs a type with all properties of T set to optional (?).

Required<T>: Constructs a type with all properties of T set to mandatory.

Readonly<T>: Makes all properties of T immutable (cannot be reassigned at compile time).

Pick<T, Keys>: Constructs a type by picking a specific set of keys from T.

TypeScript
interface Todo {
title: string;
description: string;
completed: boolean;
}

// Code Explanation:
// 'PartialTodo' treats title, description, and completed as completely optional
function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
return { ...todo, ...fieldsToUpdate };
}

// 'PreviewTodo' extracts ONLY the 'title' and 'completed' properties
type PreviewTodo = Pick<Todo, "title" | "completed">;
