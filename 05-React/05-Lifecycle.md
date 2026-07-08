## 🔹 Lifecycle

Component lifecycle refers to the stages a component goes through: **Mounting** (birth), **Updating** (growth), and **Unmounting** (death).

> 💡 In modern React, Class Component lifecycle methods (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`) are replaced entirely by the `useEffect` hook.

| Lifecycle Stage | Class Method           | Functional Hook Equivalent                                                    |
| --------------- | ---------------------- | ----------------------------------------------------------------------------- |
| Mounting        | `componentDidMount`    | `useEffect(() => {}, [])` (Empty dependency array)                            |
| Updating        | `componentDidUpdate`   | `useEffect(() => {}, [dependency])` (With dependencies)                       |
| Unmounting      | `componentWillUnmount` | `useEffect(() => { return () => { /* clean up */ } }, [])` (Cleanup function) |
