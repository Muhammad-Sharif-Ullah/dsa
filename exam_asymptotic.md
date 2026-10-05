Absolutely. Let's turn this into a **serious Big-O practice set**.

Below are **60 progressively difficult code snippets**. They are intentionally language-agnostic/normal programming problems—not Flutter. Your job for each one is to determine:

1. **Time Complexity**
2. **Space Complexity**
3. Whether the space is **auxiliary space** or includes the input
4. For recursive problems, include the **call stack**
5. Don't assume every nested loop means `O(n²)`.

**Important:** I am deliberately **not giving the answers yet**. This is meant as a hands-on exercise. After you solve them, send me your answers (even partially), and I'll grade them and explain every mistake.

---

# 🟢 Level 1 — Fundamentals

### 1

```text
function example(arr):
    x = arr[0]
    y = arr[arr.length - 1]
    return x + y
```

Find:

```text
Time: ?
Space: ?
```

---

### 2

```text
function example(arr):
    sum = 0

    for i = 0 to arr.length - 1:
        sum += arr[i]

    return sum
```

---

### 3

```text
function example(arr):
    for i = 0 to arr.length - 1:
        print(arr[i])

    for i = 0 to arr.length - 1:
        print(arr[i])
```

---

### 4

```text
function example(arr):
    for i = 0 to arr.length - 1:
        for j = 0 to arr.length - 1:
            print(arr[i], arr[j])
```

---

### 5

```text
function example(arr):
    for i = 0 to arr.length - 1:
        print(arr[i])

    for i = 0 to 9:
        print(i)
```

---

### 6

```text
function example(n):
    i = 1

    while i < n:
        print(i)
        i = i * 2
```

---

### 7

```text
function example(n):
    i = n

    while i > 1:
        print(i)
        i = i / 2
```

---

### 8

```text
function example(n):
    i = 0

    while i < n:
        j = 0

        while j < 10:
            print(i, j)
            j++

        i++
```

---

### 9

```text
function example(n):
    for i = 0 to n - 1:
        for j = 0 to i:
            print(i, j)
```

---

### 10

```text
function example(n):
    for i = 0 to n - 1:
        for j = 0 to n - 1:
            if j == i:
                print(i)
```

---

# 🟡 Level 2 — Nested Loops

### 11

```text
function example(n):
    for i = 1 to n:
        for j = 1 to i:
            print(i, j)
```

---

### 12

```text
function example(n):
    for i = 1 to n:
        j = i

        while j <= n:
            print(i, j)
            j++
```

---

### 13

```text
function example(n):
    for i = 1 to n:
        j = 1

        while j < n:
            print(i, j)
            j = j * 2
```

---

### 14

```text
function example(n):
    i = 1

    while i < n:
        for j = 0 to n - 1:
            print(i, j)

        i = i * 2
```

---

### 15

```text
function example(n):
    for i = 0 to n - 1:
        j = i

        while j > 0:
            print(i, j)
            j = j / 2
```

---

### 16

```text
function example(n):
    for i = 1 to n:
        j = 1

        while j <= i:
            print(i, j)
            j = j * 2
```

---

### 17

```text
function example(n):
    for i = 1 to n:
        j = i

        while j <= n:
            k = 1

            while k <= n:
                print(i, j, k)
                k++

            j++
```

---

### 18

```text
function example(n):
    for i = 1 to n:
        j = 1

        while j <= n:
            print(i, j)
            j = j * 2
```

---

### 19

```text
function example(n):
    i = 1

    while i <= n:
        j = 1

        while j <= i:
            print(i, j)
            j++

        i = i * 2
```

---

### 20

```text
function example(n):
    for i = 1 to n:
        for j = i to n:
            for k = j to n:
                print(i, j, k)
```

---

# 🟠 Level 3 — Multiple Inputs

For these problems, **do not automatically use `n`**.

Let:

```text
a = length of A
b = length of B
c = length of C
```

---

### 21

```text
function example(A, B):
    for i = 0 to A.length - 1:
        print(A[i])

    for j = 0 to B.length - 1:
        print(B[j])
```

---

### 22

```text
function example(A, B):
    for i = 0 to A.length - 1:
        for j = 0 to B.length - 1:
            print(A[i], B[j])
```

---

### 23

```text
function example(A, B, C):
    for x in A:
        for y in B:
            for z in C:
                print(x, y, z)
```

---

### 24

```text
function example(A, B):
    for x in A:
        for y in B:
            if x == y:
                print(x)
```

---

### 25

```text
function example(A, B):
    for x in A:
        print(x)

    for x in A:
        for y in B:
            print(x, y)

    for y in B:
        print(y)
```

---

# 🟠 Level 4 — Arrays and Searching

### 26

```text
function contains(arr, target):
    for x in arr:
        if x == target:
            return true

    return false
```

---

### 27

```text
function findMax(arr):
    max = arr[0]

    for x in arr:
        if x > max:
            max = x

    return max
```

---

### 28

```text
function containsDuplicate(arr):
    for i = 0 to arr.length - 1:
        for j = i + 1 to arr.length - 1:
            if arr[i] == arr[j]:
                return true

    return false
```

---

### 29

```text
function containsDuplicate(arr):
    seen = emptySet()

    for x in arr:
        if seen.contains(x):
            return true

        seen.add(x)

    return false
```

---

### 30

```text
function intersection(A, B):
    result = []

    for x in A:
        for y in B:
            if x == y:
                result.add(x)

    return result
```

---

# 🔴 Level 5 — Recursion

Now include **call-stack space**.

---

### 31

```text
function countdown(n):
    if n == 0:
        return

    print(n)

    countdown(n - 1)
```

---

### 32

```text
function recursive(n):
    if n <= 1:
        return 1

    return recursive(n - 1) + 1
```

---

### 33

```text
function recursive(n):
    if n <= 1:
        return

    recursive(n - 1)
    recursive(n - 1)
```

---

### 34

```text
function recursive(n):
    if n <= 1:
        return

    recursive(n - 1)
    recursive(n - 2)
```

---

### 35

```text
function recursive(n):
    if n == 0:
        return 0

    return recursive(n - 1) + n
```

---

### 36

```text
function recursive(n):
    if n <= 1:
        return n

    return recursive(n / 2)
```

---

### 37

```text
function recursive(n):
    if n <= 1:
        return

    recursive(n / 2)
    recursive(n / 2)
```

---

### 38

```text
function recursive(n):
    if n <= 1:
        return

    for i = 0 to n - 1:
        print(i)

    recursive(n / 2)
```

---

### 39

```text
function recursive(n):
    if n <= 1:
        return

    for i = 0 to n - 1:
        print(i)

    recursive(n - 1)
```

---

### 40

```text
function recursive(n):
    if n <= 1:
        return

    recursive(n / 2)

    for i = 0 to n - 1:
        print(i)

    recursive(n / 2)
```

---

# 🔴 Level 6 — Recursion + Data Structures

### 41

```text
function copy(arr, index):
    if index == arr.length:
        return

    result.add(arr[index])

    copy(arr, index + 1)
```

Assume `result` is an initially empty collection outside the function.

---

### 42

```text
function reverse(arr, left, right):
    if left >= right:
        return

    swap(arr[left], arr[right])

    reverse(arr, left + 1, right - 1)
```

---

### 43

```text
function binarySearch(arr, left, right, target):
    if left > right:
        return false

    mid = (left + right) / 2

    if arr[mid] == target:
        return true

    if target < arr[mid]:
        return binarySearch(arr, left, mid - 1, target)

    return binarySearch(arr, mid + 1, right, target)
```

---

### 44

```text
function mergeSort(arr):
    if arr.length <= 1:
        return arr

    mid = arr.length / 2

    left = mergeSort(arr[0:mid])
    right = mergeSort(arr[mid:])

    return merge(left, right)
```

Assume `merge()` takes linear time and creates a new result array.

---

### 45

```text
function permutations(arr, index):
    if index == arr.length:
        print(arr)
        return

    for i = index to arr.length - 1:
        swap(arr[index], arr[i])
        permutations(arr, index + 1)
        swap(arr[index], arr[i])
```

This one is intentionally nasty.

---

# 🔴 Level 7 — Sorting Algorithms

### 46

```text
function bubbleSort(arr):
    n = arr.length

    for i = 0 to n - 1:
        for j = 0 to n - i - 2:
            if arr[j] > arr[j + 1]:
                swap(arr[j], arr[j + 1])
```

---

### 47

```text
function selectionSort(arr):
    n = arr.length

    for i = 0 to n - 1:
        minIndex = i

        for j = i + 1 to n - 1:
            if arr[j] < arr[minIndex]:
                minIndex = j

        swap(arr[i], arr[minIndex])
```

---

### 48

```text
function insertionSort(arr):
    for i = 1 to arr.length - 1:
        key = arr[i]
        j = i - 1

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j--

        arr[j + 1] = key
```

Analyze the **worst case**.

---

### 49

```text
function sort(arr):
    if arr.length <= 1:
        return arr

    pivot = arr[0]

    left = []
    right = []

    for i = 1 to arr.length - 1:
        if arr[i] < pivot:
            left.add(arr[i])
        else:
            right.add(arr[i])

    return sort(left) + [pivot] + sort(right)
```

Analyze the **worst case**.

---

### 50

Same code as above:

```text
function sort(arr):
    if arr.length <= 1:
        return arr

    pivot = arr[0]

    left = []
    right = []

    for i = 1 to arr.length - 1:
        if arr[i] < pivot:
            left.add(arr[i])
        else:
            right.add(arr[i])

    return sort(left) + [pivot] + sort(right)
```

Now analyze the **best/balanced case**.

---

# 🟣 Level 8 — Hash Maps / Sets

### 51

```text
function findPair(arr, target):
    seen = emptySet()

    for x in arr:
        if seen.contains(target - x):
            return true

        seen.add(x)

    return false
```

Assume hash-set operations are **O(1) average**.

---

### 52

```text
function countFrequency(arr):
    map = emptyMap()

    for x in arr:
        if map.containsKey(x):
            map[x] = map[x] + 1
        else:
            map[x] = 1

    return map
```

---

### 53

```text
function groupNumbers(arr):
    groups = emptyMap()

    for x in arr:
        key = x % 10

        if !groups.containsKey(key):
            groups[key] = []

        groups[key].add(x)

    return groups
```

---

### 54

```text
function compare(A, B):
    counts = emptyMap()

    for x in A:
        counts[x]++

    for x in B:
        if counts[x] == 0:
            return false

        counts[x]--

    return true
```

---

# 🟣 Level 9 — Tricky Complexity

### 55

```text
function example(n):
    i = 0

    while i < n:
        j = i

        while j < n:
            print(i, j)
            j++

        i++
```

Don't simply say `O(n²)` without proving it.

---

### 56

```text
function example(n):
    i = 1

    while i <= n:
        j = 1

        while j <= i:
            k = 1

            while k <= j:
                print(i, j, k)
                k++

            j++

        i++
```

---

### 57

```text
function example(n):
    i = 1

    while i <= n:
        j = i

        while j <= n:
            k = 1

            while k <= j:
                print(i, j, k)
                k++

            j++

        i++
```

---

### 58

```text
function example(n):
    i = n

    while i > 0:
        j = 0

        while j < i:
            print(i, j)
            j++

        i = i / 2
```

---

### 59

```text
function example(n):
    for i = 0 to n - 1:
        j = 1

        while j < n:
            print(i, j)
            j = j * 2
```

---

### 60 — Final Boss

```text
function mystery(arr):
    n = arr.length

    for i = 0 to n - 1:

        j = 1

        while j < n:
            k = j

            while k < n:
                print(arr[i], arr[k])
                k = k * 2

            j++
```

Determine:

```text
Time: ?
Space: ?
```

Don't guess. Break down each loop mathematically.

---

# 🧠 Your Answer Format

For each problem, use this:

```text
1. Time: O(?)
   Space: O(?)
   Reason: ...

2. Time: O(?)
   Space: O(?)
   Reason: ...

3. Time: O(?)
   Space: O(?)
   Reason: ...
```

For the harder ones, I strongly recommend showing the multiplication/summation:

```text
Outer loop = ?
Inner loop = ?

Therefore:
? × ? = ?

Final:
Time = O(?)
Space = O(?)
```

### One important rule

For **space complexity**, use **auxiliary space unless the problem explicitly asks for total space**. Count things like:

- temporary arrays
- hash maps/sets
- recursion call stack
- newly created objects proportional to input

Don't count the input array itself unless the question specifically asks for total memory.

---

## Suggested challenge progression

Don't try all 60 randomly. Do:

**1–10 → fundamentals**
**11–20 → nested-loop analysis**
**21–25 → multiple inputs**
**26–30 → data structures**
**31–40 → recursion**
**41–45 → advanced recursion**
**46–50 → sorting**
**51–54 → hash-based optimization**
**55–60 → interview-level/tricky**
