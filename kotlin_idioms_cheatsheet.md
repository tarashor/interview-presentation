# Kotlin Idioms Cheatsheet

This cheatsheet is compiled directly from your private LeetCode and programming solutions in the [src](file:///Users/tarasgoriachko/projects/private/interview/src) directory. We scanned all `.kt` files to extract the Kotlin constructs you use the most, providing a cheatsheet tailored to your actual coding style.

---

## 📊 Your Top Kotlin Idioms at a Glance

| Idiom / Construct | Count | Primary Use Case in Your Code | Codebase Example |
| :--- | :--- | :--- | :--- |
| **`intArrayOf` / `arrayOf`** | **355** | Declaring inputs and 2D matrices in tests. | `intArrayOf(2, 7, 11, 15)` |
| **`until` operator** | **87** | Iterating forward from `0` to `size - 1` (exclusive boundary). | `for (i in 0 until nums.size)` |
| **Safe Call (`?.`)** | **78** | Null-safe node traversal in trees and lists. | `cur1 = cur1?.next` |
| **`kotlin.math` (min/max/abs)** | **68** | Coordinate calculations and range clamping. | `kotlin.math.min(price, minPrice)` |
| **`mutableListOf` / `listOf`** | **77** | Dynamically building outputs and collections. | `val res = mutableListOf<List<Int>>()` |
| **`apply` scope function** | **40** | Building test inputs, especially linked lists and trees. | `ListNode(3).apply { next = ListNode(1) }` |
| **`getOrDefault`** | **24** | Accessing map values with fallback (great for graphs/counters). | `adj.getOrDefault(v, hashMapOf())` |
| **`ArrayDeque`** | **20** | BFS queue queueing and Stack implementation. | `val deque = ArrayDeque<IntArray>()` |
| **`return if` (Expression)** | **19** | Cleaner conditional returns without temporary variables. | `return if (val1 >= 0) val1 else val2` |
| **Elvis Operator (`?:`)** | **14** | Null-safe fallback values. | `(l1?.`val` ?: 0)` |

---

## 🛠️ Idiom Cheatsheet & Code Patterns

### 1. Loop Boundaries & Iteration
You almost exclusively use Kotlin's range operators and custom loop styles rather than traditional C-style loops.

*   **Forward Loop (Exclusive Upper Bound):** Use `until` to avoid index-out-of-bounds.
    ```kotlin
    for (i in 0 until nums.size) { ... }
    ```
*   **Backward Loop (Inclusive Lower Bound):** Use `downTo` to loop backwards.
    ```kotlin
    for (r in board.size - 1 downTo 0) { ... }
    ```
*   **Accessing both index and element:** Use `forEachIndexed` instead of tracking a manual counter.
    ```kotlin
    nums.forEachIndexed { index, num ->
        // use index and num
    }
    ```
*   **Map Iteration:** Destructure maps directly in loops.
    ```kotlin
    for ((key, value) in map) {
        max = kotlin.math.max(max, value)
    }
    ```

### 2. Scope Functions (`apply` and `let`)
Scope functions make your object configuration and null checks highly readable.

*   **Linked List / Tree Builder Pattern:** You use nested `.apply {}` calls in tests to assemble linked structures cleanly.
    ```kotlin
    val list = ListNode(3).apply {
        next = ListNode(1).apply {
            next = ListNode(2)
        }
    }
    ```
*   **Null-Safe Processing (`?.let`):** Execute a block only if the checked object is not null.
    ```kotlin
    map[target - num]?.let { index ->
        return intArrayOf(index, currentIdx)
    }
    ```

### 3. Collection & Array Initializers
Dynamic array creation with initializers is one of your strongest patterns for DP tables.

*   **1D Array with Default Value:**
    ```kotlin
    val maxDistance = IntArray(size) { Int.MIN_VALUE }
    val usedChars = BooleanArray(26) { false }
    ```
*   **2D Array / DP Matrix Initializer:** Use the lambda initializer syntax instead of nested loops.
    ```kotlin
    val dp = Array<IntArray>(obstacleGrid.size) { row ->
        IntArray(obstacleGrid[row].size) { col ->
            if (row == 0 && col == 0) 1 else 0
        }
    }
    ```

### 4. Null Safety & Fallbacks
*   **The Elvis Operator (`?:`):** Provide immediate defaults for optional fields or nullable nodes.
    ```kotlin
    val res = (l1?.`val` ?: 0) + (l2?.`val` ?: 0) + carry
    ```
*   **Double Bang (`!!`):** Use when you have manually validated that an item is not null (e.g., getting a map entry that must exist).
    ```kotlin
    val minEntry = basket.minByOrNull { it.value }!!
    ```

### 5. Advanced Kotlin Idioms for Coding Problems
*   **Returning `if` / `when` as Expressions:** Keep your code branching flat.
    ```kotlin
    return if (minPrice == Int.MAX_VALUE) -1 else minPrice
    ```
*   **Single-Expression Functions:** For short utility methods.
    ```kotlin
    fun top(): Int = stack.peek()
    fun getMin(): Int = minStack.peek()
    ```
*   **Pair Infix (`to`):** Quick creation of key-value pairs or tuples.
    ```kotlin
    return ListNode(res % 10) to res / 10
    ```
*   **Destructuring Declarations:** Unpack pairs/tuples directly into descriptive variables.
    ```kotlin
    val (node, carry) = add(cur1, cur2, carry)
    ```
*   **Collection Extras (`last()`, `removeLast()`):**
    ```kotlin
    // Standard Kotlin array utility
    val lastRow = obstacleGrid.last()
    
    // Creating custom extension functions on StringBuilder
    private fun StringBuilder.removeLast() {
        setLength(lastIndex)
    }
    ```
