# Data Structures & Algorithms: Zero-to-Confident Roadmap

Oct 5, 2026 · @Md Sharif Ullah

## How to use this roadmap

Work through 11 phases in order over about 16 weeks at 1–2 hours a day, using only free resources. Each phase builds on the one before it, so do not skip ahead until you can solve that phase's easy problems without help.

&#91;embedded content: DSA roadmap · 11 phases over 16 weeks\]

The weeks are a guide: if a phase takes longer, stay with it rather than rushing to the next.

All code examples are in Python because most free courses and problem solutions use it. The ideas transfer directly to Dart, Kotlin, Swift, C++ or Java.

**The learning loop for every topic**

1. **Learn** the idea from one video or article (links in each phase).
2. **See it** move step by step in [VisuAlgo](https://visualgo.net/en) or [Python Tutor](https://pythontutor.com/).
3. **Build it** from scratch without copying, then compare with the example in this doc.
4. **Practice** the listed problems in order, easy first.
5. **Review** each solved problem again after 2 days and after 1 week.

**The stuck rule:** try a problem for 25–30 minutes. If you are still stuck, read only a hint, then the solution. Write the solution again yourself the next day without looking.

**Free practice platforms**

| Platform   | Best for                                                     | Link                                                                 |
| ---------- | ------------------------------------------------------------ | -------------------------------------------------------------------- |
| LeetCode   | Interview-style problems, the main practice list in this doc | [leetcode.com](https://leetcode.com/problemset/)                     |
| NeetCode   | Problems grouped by pattern, with free video solutions       | [neetcode.io/roadmap](https://neetcode.io/roadmap)                   |
| HackerRank | Gentle beginner problems with guided tracks                  | [hackerrank.com](https://www.hackerrank.com/domains/data-structures) |
| CSES       | 300 classic algorithm problems, great after Phase 8          | [cses.fi/problemset](https://cses.fi/problemset/)                    |
| Codeforces | Timed contests once you are comfortable                      | [codeforces.com](https://codeforces.com/)                            |

Links are from knowledge as of mid-2026; if one has moved, search the resource name.

## Phase 0: Prerequisites and Big-O (Week 1)

Big-O tells you how an algorithm's time or memory grows as input size n grows. It is the language you will use to judge every solution in this course.

**What you must know before starting:** variables, loops, functions, lists, dictionaries, classes, and basic recursion in one language.

**Core ideas**

- **O(1)** constant: reading `arr[5]`.
- **O(log n)** logarithmic: halving the search space each step (binary search).
- **O(n)** linear: one loop over the input.
- **O(n log n)**: efficient sorting (merge sort).
- **O(n²)** quadratic: a loop inside a loop.
- **O(2ⁿ)** exponential: trying every subset.
- Drop constants and smaller terms: O(3n + 10) becomes O(n).

**Hands-on example: the same problem, two speeds**

Check whether a list has a duplicate.

```python
# O(n^2) time, O(1) space: compare every pair
def has_duplicate_slow(nums):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] == nums[j]:
                return True
    return False

# O(n) time, O(n) space: remember what we have seen
def has_duplicate_fast(nums):
    seen = set()
    for x in nums:
        if x in seen:
            return True
        seen.add(x)
    return False
```

For 1,000,000 numbers, the slow version does about 500 billion comparisons; the fast one does 1 million lookups. That trade of memory for speed appears again and again.

**Exercise:** write down the Big-O of each function you write this week before running it.

**Free resources**

- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/) — complexity table for common structures and sorts
- [Abdul Bari: Algorithms (YouTube)](https://www.youtube.com/@abdul_bari) — start with the asymptotic notation videos
- [CS50x (Harvard)](https://cs50.harvard.edu/x/) — free course if you need to strengthen programming basics first
- [Python Tutor](https://pythontutor.com/) — watch your code run line by line

**Practice:** [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) · [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) · [Single Number](https://leetcode.com/problems/single-number/)

## Phase 1: Arrays and strings (Weeks 2–3)

Arrays are the base of almost every other structure, and three patterns solve most array problems: two pointers, sliding window and prefix sums.

**Core ideas**

- Index access is O(1); inserting or deleting in the middle is O(n) because items shift.
- Python strings are immutable: build with a list and `''.join()` instead of `+=` in a loop.
- **Two pointers:** one pointer at each end (or a slow and a fast pointer) moving toward each other.
- **Sliding window:** a moving range `[left, right]` that grows and shrinks to keep a condition true.
- **Prefix sums:** precompute running totals so any range sum is O(1).

**Hands-on example 1: two pointers (sorted Two Sum)**

```python
def two_sum_sorted(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        total = nums[left] + nums[right]
        if total == target:
            return [left, right]
        if total < target:
            left += 1      # need a bigger sum
        else:
            right -= 1     # need a smaller sum
    return []

print(two_sum_sorted([1, 3, 4, 6, 9], 10))  # [0, 4] -> 1 + 9
```

**Hands-on example 2: sliding window (longest substring without repeats)**

```python
def longest_unique(s):
    seen = set()
    left = best = 0
    for right, ch in enumerate(s):
        while ch in seen:          # shrink until window is valid
            seen.remove(s[left])
            left += 1
        seen.add(ch)
        best = max(best, right - left + 1)
    return best

print(longest_unique("abcabcbb"))  # 3 -> "abc"
```

**Hands-on example 3: prefix sums**

```python
nums = [2, 4, 1, 3, 5]
prefix = [0]
for x in nums:
    prefix.append(prefix[-1] + x)   # [0, 2, 6, 7, 10, 15]

def range_sum(i, j):                # sum of nums[i..j]
    return prefix[j + 1] - prefix[i]

print(range_sum(1, 3))  # 4 + 1 + 3 = 8
```

**Free resources**

- [NeetCode: Arrays & Hashing and Two Pointers playlists](https://neetcode.io/roadmap) — video walkthrough of each problem below
- [VisuAlgo: Array](https://visualgo.net/en/array) — animated insert, delete and search
- [LeetCode Patterns by Sean Prashad](https://seanprashad.com/leetcode-patterns/) — filter problems by pattern

**Practice (in order)**

| #   | Problem                                                                                                                         | Pattern             | Level  |
| --- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------- | ------ |
| 1   | [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)                                                             | Two pointers        | Easy   |
| 2   | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)                               | One pass            | Easy   |
| 3   | [Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)                                                   | Two pointers        | Medium |
| 4   | [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/)                                         | Prefix sums         | Easy   |
| 5   | [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)                                     | Prefix and suffix   | Medium |
| 6   | [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)                                           | Two pointers        | Medium |
| 7   | [3Sum](https://leetcode.com/problems/3sum/)                                                                                     | Sort + two pointers | Medium |
| 8   | [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | Sliding window      | Medium |
| 9   | [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)               | Sliding window      | Medium |

## Phase 2: Hashing (Week 4)

A hash map turns "search the whole list" into an O(1) average lookup, which is why it is the single most useful tool in interviews and real apps.

**Core ideas**

- A hash function maps a key to a bucket index; collisions are handled by chaining or open addressing.
- `dict` (key → value) and `set` (keys only) in Python; `Map` and `Set` in Dart.
- Average O(1) insert, delete and lookup; worst case O(n) with many collisions.
- Counting with `collections.Counter` and grouping with `defaultdict(list)` are everyday patterns.

**Hands-on example 1: Two Sum (the classic)**

```python
def two_sum(nums, target):
    index_of = {}                      # value -> index
    for i, x in enumerate(nums):
        need = target - x
        if need in index_of:
            return [index_of[need], i]
        index_of[x] = i
    return []

print(two_sum([2, 7, 11, 15], 9))  # [0, 1]
```

**Hands-on example 2: group anagrams with a signature key**

```python
from collections import defaultdict

def group_anagrams(words):
    groups = defaultdict(list)
    for w in words:
        groups["".join(sorted(w))].append(w)   # "eat" -> "aet"
    return list(groups.values())

print(group_anagrams(["eat", "tea", "tan", "ate", "nat", "bat"]))
# [['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

**Build it yourself:** write a tiny `MyHashMap` class with a list of 1,000 buckets, `put`, `get` and `remove`, using chaining. Test it on [Design HashMap](https://leetcode.com/problems/design-hashmap/).

**Free resources**

- [VisuAlgo: Hash Table](https://visualgo.net/en/hashtable) — see collisions and probing
- [Python docs: collections](https://docs.python.org/3/library/collections.html) — `Counter`, `defaultdict`, `deque`
- [NeetCode roadmap: Arrays & Hashing](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                                                     | Idea                | Level  |
| --- | ------------------------------------------------------------------------------------------- | ------------------- | ------ |
| 1   | [Two Sum](https://leetcode.com/problems/two-sum/)                                           | Complement lookup   | Easy   |
| 2   | [Valid Anagram](https://leetcode.com/problems/valid-anagram/)                               | Counting            | Easy   |
| 3   | [Design HashMap](https://leetcode.com/problems/design-hashmap/)                             | Build the structure | Easy   |
| 4   | [Group Anagrams](https://leetcode.com/problems/group-anagrams/)                             | Signature key       | Medium |
| 5   | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)           | Count + bucket      | Medium |
| 6   | [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)               | Prefix sum + map    | Medium |
| 7   | [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) | Set lookups         | Medium |

## Phase 3: Linked lists, stacks and queues (Weeks 5–6)

These three structures teach you to think in pointers and in order of processing: last-in-first-out (stack) versus first-in-first-out (queue).

**Core ideas**

- **Linked list:** nodes holding a value and a `next` pointer. O(1) insert at a known node, O(n) to find a position.
- Tricks: a dummy head node, slow/fast pointers (cycle detection, middle node), reversing in place.
- **Stack:** push and pop at one end. Python `list` with `append` and `pop`. Used for undo, brackets, expression parsing.
- **Monotonic stack:** keeps items in increasing or decreasing order to find the "next greater" item in O(n).
- **Queue:** add at the back, remove at the front. Use `collections.deque` (O(1) both ends), never `list.pop(0)`.

**Hands-on example 1: reverse a linked list**

```python
class Node:
    def __init__(self, val, next=None):
        self.val, self.next = val, next

def reverse(head):
    prev = None
    while head:
        nxt = head.next      # save the rest
        head.next = prev     # flip the arrow
        prev, head = head, nxt
    return prev

# 1 -> 2 -> 3  becomes  3 -> 2 -> 1
```

**Hands-on example 2: stack for valid brackets**

```python
def is_valid(s):
    pairs = {')': '(', ']': '[', '}': '{'}
    stack = []
    for ch in s:
        if ch in pairs:
            if not stack or stack.pop() != pairs[ch]:
                return False
        else:
            stack.append(ch)
    return not stack

print(is_valid("([]{})"), is_valid("(]"))  # True False
```

**Hands-on example 3: monotonic stack (days until a warmer day)**

```python
def daily_temperatures(temps):
    answer = [0] * len(temps)
    stack = []                         # indexes, temps decreasing
    for i, t in enumerate(temps):
        while stack and temps[stack[-1]] < t:
            j = stack.pop()
            answer[j] = i - j
        stack.append(i)
    return answer

print(daily_temperatures([73, 74, 75, 71, 69, 72, 76]))
# [1, 1, 4, 2, 1, 1, 0]
```

**Free resources**

- [VisuAlgo: Linked List, Stack, Queue, Deque](https://visualgo.net/en/list)
- [Open Data Structures (free book)](https://opendatastructures.org/) — chapters on lists, stacks and queues
- [NeetCode roadmap: Stack and Linked List](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                                                             | Structure                     | Level  |
| --- | --------------------------------------------------------------------------------------------------- | ----------------------------- | ------ |
| 1   | [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)                           | Linked list                   | Easy   |
| 2   | [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)                     | Dummy head                    | Easy   |
| 3   | [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)                               | Slow/fast pointers            | Easy   |
| 4   | [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)                               | Stack                         | Easy   |
| 5   | [Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)         | Stack + queue                 | Easy   |
| 6   | [Min Stack](https://leetcode.com/problems/min-stack/)                                               | Stack design                  | Medium |
| 7   | [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) | Two pointers                  | Medium |
| 8   | [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)                             | Monotonic stack               | Medium |
| 9   | [LRU Cache](https://leetcode.com/problems/lru-cache/)                                               | Hash map + doubly linked list | Medium |

## Phase 4: Recursion and backtracking (Week 7)

Recursion solves a problem by solving smaller copies of it, and backtracking is recursion that tries a choice, explores it, then undoes it. Trees, graphs and dynamic programming all depend on this phase.

**Core ideas**

- Every recursive function needs a **base case** (when to stop) and a **recursive case** (a smaller step).
- Each call sits on the call stack; deep recursion can overflow it (Python's default limit is about 1,000 calls).
- **Backtracking template:** choose → explore → un-choose.
- Draw the recursion tree on paper for small inputs; it shows both the answer and the time complexity.

**Hands-on example 1: recursion basics**

```python
def power(base, exp):
    if exp == 0:                 # base case
        return 1
    half = power(base, exp // 2) # smaller problem
    return half * half * (base if exp % 2 else 1)

print(power(2, 10))  # 1024, in O(log n) calls
```

**Hands-on example 2: backtracking template (all subsets)**

```python
def subsets(nums):
    result, path = [], []

    def backtrack(start):
        result.append(path[:])          # record current choice set
        for i in range(start, len(nums)):
            path.append(nums[i])        # choose
            backtrack(i + 1)            # explore
            path.pop()                  # un-choose

    backtrack(0)
    return result

print(subsets([1, 2, 3]))
# [[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
```

The same template, with small changes, solves permutations, combination sum, word search and N-Queens.

**Free resources**

- [Abdul Bari: Recursion and backtracking videos](https://www.youtube.com/@abdul_bari)
- [Python Tutor](https://pythontutor.com/) — watch the call stack grow and shrink
- [NeetCode roadmap: Backtracking](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                             | Idea                  | Level  |
| --- | ------------------------------------------------------------------- | --------------------- | ------ |
| 1   | [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) | Plain recursion       | Easy   |
| 2   | [Pow(x, n)](https://leetcode.com/problems/powx-n/)                  | Divide in half        | Medium |
| 3   | [Subsets](https://leetcode.com/problems/subsets/)                   | Backtracking template | Medium |
| 4   | [Permutations](https://leetcode.com/problems/permutations/)         | Used-set              | Medium |
| 5   | [Combination Sum](https://leetcode.com/problems/combination-sum/)   | Reuse choices         | Medium |
| 6   | [Word Search](https://leetcode.com/problems/word-search/)           | Grid backtracking     | Medium |
| 7   | [N-Queens](https://leetcode.com/problems/n-queens/)                 | Pruning               | Hard   |

## Phase 5: Sorting and binary search (Week 8)

Sorting puts data in order so later work is fast, and binary search uses that order to find anything in O(log n): about 20 steps for a million items.

**Core ideas**

- Learn by hand: bubble, selection and insertion sort (O(n²)), then merge sort and quick sort (O(n log n)).
- **Stable** sorts keep equal items in their original order (merge sort is stable; quick sort usually is not).
- In real code, use the built-in `sorted()` / `list.sort()` (Timsort, O(n log n)).
- **Binary search** needs sorted data or any yes/no condition that flips once (false, false, true, true).
- **Binary search on the answer:** search over possible answers, not over the array (Koko Eating Bananas).

**Hands-on example 1: merge sort (divide and conquer)**

```python
def merge_sort(a):
    if len(a) <= 1:
        return a
    mid = len(a) // 2
    left, right = merge_sort(a[:mid]), merge_sort(a[mid:])
    merged, i, j = [], 0, 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i]); i += 1
        else:
            merged.append(right[j]); j += 1
    return merged + left[i:] + right[j:]

print(merge_sort([5, 2, 9, 1, 5, 6]))  # [1, 2, 5, 5, 6, 9]
```

**Hands-on example 2: a binary search template you can trust**

```python
def first_true(lo, hi, condition):
    """Smallest x in [lo, hi] where condition(x) is True."""
    while lo < hi:
        mid = (lo + hi) // 2
        if condition(mid):
            hi = mid          # answer is mid or left of it
        else:
            lo = mid + 1      # answer is right of mid
    return lo

nums = [1, 3, 5, 7, 9]
print(first_true(0, len(nums), lambda i: nums[i] >= 7))  # 3
```

The same `first_true` function solves Search Insert Position, First Bad Version and Koko Eating Bananas by changing only the condition.

**Free resources**

- [VisuAlgo: Sorting](https://visualgo.net/en/sorting) — animate every sort side by side
- [MIT 6.006 Introduction to Algorithms (OCW)](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) — lectures on sorting and searching
- [NeetCode roadmap: Binary Search](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                                                         | Idea             | Level  |
| --- | ----------------------------------------------------------------------------------------------- | ---------------- | ------ |
| 1   | [Binary Search](https://leetcode.com/problems/binary-search/)                                   | Basic template   | Easy   |
| 2   | [Search Insert Position](https://leetcode.com/problems/search-insert-position/)                 | First true       | Easy   |
| 3   | [Sort an Array](https://leetcode.com/problems/sort-an-array/)                                   | Write merge sort | Medium |
| 4   | [Sort Colors](https://leetcode.com/problems/sort-colors/)                                       | Three pointers   | Medium |
| 5   | [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)                       | Search on answer | Medium |
| 6   | [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) | Modified search  | Medium |
| 7   | [Merge Intervals](https://leetcode.com/problems/merge-intervals/)                               | Sort then sweep  | Medium |

## Phase 6: Trees and binary search trees (Weeks 9–10)

A tree is a hierarchy of nodes with no cycles, and nearly every tree problem is solved by one of two traversals: depth-first (recursion) or breadth-first (a queue).

**Core ideas**

- Terms: root, parent, child, leaf, height, depth, subtree.
- **DFS orders:** preorder (node, left, right), inorder (left, node, right), postorder (left, right, node).
- **BFS / level order:** visit level by level with a `deque`.
- **Binary search tree (BST):** left < node < right. Search, insert and delete are O(log n) when balanced, O(n) when skewed.
- Inorder traversal of a BST gives sorted order — a key trick for BST problems.
- Real-world trees: file systems, UI widget trees (Flutter, the DOM), game scene graphs.

**Hands-on example 1: DFS — maximum depth**

```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val, self.left, self.right = val, left, right

def max_depth(root):
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))
```

**Hands-on example 2: BFS — level order**

```python
from collections import deque

def level_order(root):
    if not root:
        return []
    levels, queue = [], deque([root])
    while queue:
        level = []
        for _ in range(len(queue)):     # one full level
            node = queue.popleft()
            level.append(node.val)
            if node.left:  queue.append(node.left)
            if node.right: queue.append(node.right)
        levels.append(level)
    return levels
```

**Hands-on example 3: BST insert and search**

```python
def insert(root, val):
    if not root:
        return TreeNode(val)
    if val < root.val:
        root.left = insert(root.left, val)
    else:
        root.right = insert(root.right, val)
    return root

def search(root, val):
    while root and root.val != val:
        root = root.left if val < root.val else root.right
    return root is not None

root = None
for v in [8, 3, 10, 1, 6, 14]:
    root = insert(root, v)
print(search(root, 6), search(root, 7))  # True False
```

**Free resources**

- [VisuAlgo: Binary Search Tree / AVL](https://visualgo.net/en/bst)
- [Abdul Bari: Trees and AVL rotations](https://www.youtube.com/@abdul_bari)
- [NeetCode roadmap: Trees](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                                                                          | Idea           | Level  |
| --- | ---------------------------------------------------------------------------------------------------------------- | -------------- | ------ |
| 1   | [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)                      | DFS            | Easy   |
| 2   | [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)                                          | DFS            | Easy   |
| 3   | [Same Tree](https://leetcode.com/problems/same-tree/)                                                            | Two-tree DFS   | Easy   |
| 4   | [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)            | BFS            | Medium |
| 5   | [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)                        | Min/max bounds | Medium |
| 6   | [Lowest Common Ancestor of a BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) | BST property   | Medium |
| 7   | [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)                    | Inorder        | Medium |
| 8   | [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)                      | Postorder      | Hard   |

## Phase 7: Heaps and priority queues (Week 11)

A heap always gives you the smallest (or largest) item in O(1) and adds or removes items in O(log n), which makes it the tool for "top K", "next most urgent" and scheduling problems.

**Core ideas**

- A binary heap is a complete tree stored in an array: children of index i are at 2i + 1 and 2i + 2.
- **Min-heap:** parent ≤ children. Python's `heapq` is a min-heap; push `-x` to simulate a max-heap.
- `heappush` and `heappop` are O(log n); `heapify` builds a heap from a list in O(n).
- **Top-K pattern:** keep a min-heap of size k; the root is the kth largest seen so far.
- **Two-heap pattern:** a max-heap for the lower half and a min-heap for the upper half gives a running median.
- Game use: turn order by speed, event schedulers, and the open list in A\* pathfinding.

**Hands-on example 1: kth largest with a size-k heap**

```python
import heapq

def kth_largest(nums, k):
    heap = []
    for x in nums:
        heapq.heappush(heap, x)
        if len(heap) > k:
            heapq.heappop(heap)   # drop the smallest
    return heap[0]

print(kth_largest([3, 2, 1, 5, 6, 4], 2))  # 5
```

**Hands-on example 2: a task scheduler by priority**

```python
import heapq

tasks = []
heapq.heappush(tasks, (2, "write tests"))
heapq.heappush(tasks, (1, "fix crash"))
heapq.heappush(tasks, (3, "update docs"))

while tasks:
    priority, name = heapq.heappop(tasks)
    print(priority, name)
# 1 fix crash / 2 write tests / 3 update docs
```

**Free resources**

- [VisuAlgo: Binary Heap](https://visualgo.net/en/heap) — watch sift-up and sift-down
- [Python docs: heapq](https://docs.python.org/3/library/heapq.html)
- [NeetCode roadmap: Heap / Priority Queue](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                                                           | Idea           | Level  |
| --- | ------------------------------------------------------------------------------------------------- | -------------- | ------ |
| 1   | [Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)                             | Max-heap       | Easy   |
| 2   | [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/) | Size-k heap    | Easy   |
| 3   | [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | Size-k heap    | Medium |
| 4   | [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)           | Heap of tuples | Medium |
| 5   | [Task Scheduler](https://leetcode.com/problems/task-scheduler/)                                   | Greedy + heap  | Medium |
| 6   | [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)                       | K-way merge    | Hard   |
| 7   | [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)       | Two heaps      | Hard   |

## Phase 8: Graphs (Weeks 12–13)

A graph is a set of nodes connected by edges, and five algorithms cover most graph problems: BFS, DFS, topological sort, Dijkstra and union-find.

**Core ideas**

- Store graphs as an **adjacency list**: `graph = {node: [neighbors]}`. A 2D grid is also a graph (each cell links to up, down, left, right).
- Directed vs undirected; weighted vs unweighted; cyclic vs acyclic.
- **BFS** (queue) finds the shortest path when every edge costs the same.
- **DFS** (recursion or stack) explores connected regions, detects cycles, and powers flood fill.
- **Topological sort** orders tasks that depend on each other (course prerequisites, build steps).
- **Dijkstra** (heap) finds the shortest path with non-negative weights; **A\*** adds a distance guess and is the standard for game pathfinding.
- **Union-find** answers "are these two connected?" almost in O(1).

**Hands-on example 1: BFS shortest path on a grid**

```python
from collections import deque

def shortest_path(grid, start, goal):
    rows, cols = len(grid), len(grid[0])
    queue, seen = deque([(start, 0)]), {start}
    while queue:
        (r, c), dist = queue.popleft()
        if (r, c) == goal:
            return dist
        for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols \
               and grid[nr][nc] == 0 and (nr, nc) not in seen:
                seen.add((nr, nc))
                queue.append(((nr, nc), dist + 1))
    return -1

grid = [[0, 0, 0],
        [1, 1, 0],
        [0, 0, 0]]      # 1 = wall
print(shortest_path(grid, (0, 0), (2, 0)))  # 6
```

**Hands-on example 2: topological sort (Kahn's algorithm)**

```python
from collections import deque, defaultdict

def course_order(n, prereqs):
    graph, indegree = defaultdict(list), [0] * n
    for course, before in prereqs:
        graph[before].append(course)
        indegree[course] += 1
    queue = deque(i for i in range(n) if indegree[i] == 0)
    order = []
    while queue:
        node = queue.popleft()
        order.append(node)
        for nxt in graph[node]:
            indegree[nxt] -= 1
            if indegree[nxt] == 0:
                queue.append(nxt)
    return order if len(order) == n else []   # [] means a cycle

print(course_order(4, [[1, 0], [2, 0], [3, 1], [3, 2]]))  # [0, 1, 2, 3]
```

**Hands-on example 3: Dijkstra**

```python
import heapq

def dijkstra(graph, source):
    dist = {source: 0}
    heap = [(0, source)]
    while heap:
        d, node = heapq.heappop(heap)
        if d > dist.get(node, float("inf")):
            continue                        # stale entry
        for nxt, weight in graph[node]:
            nd = d + weight
            if nd < dist.get(nxt, float("inf")):
                dist[nxt] = nd
                heapq.heappush(heap, (nd, nxt))
    return dist

graph = {"A": [("B", 4), ("C", 1)], "B": [("D", 1)],
         "C": [("B", 2), ("D", 5)], "D": []}
print(dijkstra(graph, "A"))  # {'A': 0, 'B': 3, 'C': 1, 'D': 4}
```

**Hands-on example 4: union-find**

```python
parent = list(range(10))

def find(x):
    while parent[x] != x:
        parent[x] = parent[parent[x]]   # path compression
        x = parent[x]
    return x

def union(a, b):
    ra, rb = find(a), find(b)
    if ra == rb:
        return False                    # already connected: a cycle
    parent[ra] = rb
    return True
```

**Free resources**

- [Red Blob Games: Introduction to A\*](https://www.redblobgames.com/pathfinding/a-star/introduction.html) — interactive BFS, Dijkstra and A\*, written for game developers
- [VisuAlgo: Graph Traversal](https://visualgo.net/en/dfsbfs) and [Shortest Paths](https://visualgo.net/en/sssp)
- [CP-Algorithms: Graphs](https://cp-algorithms.com/) — reference for every classic graph algorithm
- [NeetCode roadmap: Graphs](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                                                         | Algorithm        | Level  |
| --- | ----------------------------------------------------------------------------------------------- | ---------------- | ------ |
| 1   | [Flood Fill](https://leetcode.com/problems/flood-fill/)                                         | DFS on grid      | Easy   |
| 2   | [Number of Islands](https://leetcode.com/problems/number-of-islands/)                           | DFS/BFS          | Medium |
| 3   | [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)                               | Multi-source BFS | Medium |
| 4   | [Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/) | BFS              | Medium |
| 5   | [Clone Graph](https://leetcode.com/problems/clone-graph/)                                       | DFS + map        | Medium |
| 6   | [Course Schedule](https://leetcode.com/problems/course-schedule/)                               | Topological sort | Medium |
| 7   | [Number of Provinces](https://leetcode.com/problems/number-of-provinces/)                       | Union-find       | Medium |
| 8   | [Redundant Connection](https://leetcode.com/problems/redundant-connection/)                     | Union-find       | Medium |
| 9   | [Network Delay Time](https://leetcode.com/problems/network-delay-time/)                         | Dijkstra         | Medium |

## Phase 9: Dynamic programming (Weeks 14–15)

Dynamic programming (DP) is recursion that remembers answers to repeated subproblems, turning exponential solutions into polynomial ones. It feels hard at first; a fixed 4-step recipe makes it manageable.

**The 4-step recipe**

1. **Define the state:** what does `dp[i]` (or `dp[i][j]`) mean in words?
2. **Write the transition:** how is `dp[i]` built from smaller states?
3. **Set the base cases:** the smallest answers you know directly.
4. **Choose the order:** top-down (recursion + memo) or bottom-up (fill a table).

**Common DP families:** 1D (climbing stairs, house robber), 2D grid (unique paths), knapsack (coin change, partition subset), two strings (LCS, edit distance), and subsequences (LIS).

**Hands-on example 1: the same problem three ways (climbing stairs)**

```python
from functools import lru_cache

# 1. Plain recursion: O(2^n), too slow for n = 40
def climb_slow(n):
    return 1 if n <= 1 else climb_slow(n - 1) + climb_slow(n - 2)

# 2. Top-down with memo: O(n)
@lru_cache(maxsize=None)
def climb_memo(n):
    return 1 if n <= 1 else climb_memo(n - 1) + climb_memo(n - 2)

# 3. Bottom-up with two variables: O(n) time, O(1) space
def climb(n):
    a, b = 1, 1
    for _ in range(n - 1):
        a, b = b, a + b
    return b

print(climb(5))  # 8
```

**Hands-on example 2: coin change (unbounded knapsack)**

```python
def coin_change(coins, amount):
    # dp[x] = fewest coins to make amount x
    dp = [0] + [float("inf")] * amount
    for x in range(1, amount + 1):
        for c in coins:
            if c <= x:
                dp[x] = min(dp[x], dp[x - c] + 1)
    return dp[amount] if dp[amount] != float("inf") else -1

print(coin_change([1, 2, 5], 11))  # 3 -> 5 + 5 + 1
```

**Hands-on example 3: longest common subsequence (2D table)**

```python
def lcs(a, b):
    # dp[i][j] = LCS of a[:i] and b[:j]
    dp = [[0] * (len(b) + 1) for _ in range(len(a) + 1)]
    for i in range(1, len(a) + 1):
        for j in range(1, len(b) + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    return dp[-1][-1]

print(lcs("abcde", "ace"))  # 3
```

**Free resources**

- [freeCodeCamp: Dynamic Programming course (YouTube)](https://www.youtube.com/@freecodecamp) — search "Dynamic Programming for Beginners" on the channel
- [MIT 6.006 (OCW): DP lectures](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) — the SRTBOT method for designing DP
- [NeetCode roadmap: 1-D and 2-D Dynamic Programming](https://neetcode.io/roadmap)
- [CSES Problem Set: Dynamic Programming section](https://cses.fi/problemset/) — classic DP problems for extra practice

**Practice (in order)**

| #   | Problem                                                                                         | Family             | Level  |
| --- | ----------------------------------------------------------------------------------------------- | ------------------ | ------ |
| 1   | [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)                               | 1D                 | Easy   |
| 2   | [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)             | 1D                 | Easy   |
| 3   | [House Robber](https://leetcode.com/problems/house-robber/)                                     | 1D choice          | Medium |
| 4   | [Unique Paths](https://leetcode.com/problems/unique-paths/)                                     | 2D grid            | Medium |
| 5   | [Coin Change](https://leetcode.com/problems/coin-change/)                                       | Unbounded knapsack | Medium |
| 6   | [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)         | 0/1 knapsack       | Medium |
| 7   | [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) | Subsequence        | Medium |
| 8   | [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)         | Two strings        | Medium |
| 9   | [Edit Distance](https://leetcode.com/problems/edit-distance/)                                   | Two strings        | Medium |

## Phase 10: Greedy, tries and advanced topics (Week 16)

Greedy algorithms make the best local choice at each step, tries make prefix search fast, and bit manipulation solves some problems in a single pass. After this phase you have covered the full standard DSA syllabus.

**Core ideas**

- **Greedy** works only when a local best choice never hurts the final answer; test it on small counterexamples before trusting it.
- **Intervals:** sort by start or end, then sweep once (meeting rooms, merging ranges).
- **Trie (prefix tree):** each node is a character; insert and search are O(length of word). Used for autocomplete and word games.
- **Bit manipulation:** `x & 1` (odd?), `x & (x - 1)` (drops the lowest set bit), `a ^ a = 0` (find the single number).
- **Optional advanced topics** once the above feel easy: segment tree, Fenwick tree, KMP string matching, minimum spanning tree (Kruskal, Prim), bitmask DP.

**Hands-on example 1: greedy (Jump Game)**

```python
def can_jump(nums):
    reach = 0                      # farthest index reachable so far
    for i, step in enumerate(nums):
        if i > reach:
            return False
        reach = max(reach, i + step)
    return True

print(can_jump([2, 3, 1, 1, 4]), can_jump([3, 2, 1, 0, 4]))  # True False
```

**Hands-on example 2: trie for autocomplete**

```python
class Trie:
    def __init__(self):
        self.children, self.is_word = {}, False

    def insert(self, word):
        node = self
        for ch in word:
            node = node.children.setdefault(ch, Trie())
        node.is_word = True

    def starts_with(self, prefix):
        node = self
        for ch in prefix:
            if ch not in node.children:
                return []
            node = node.children[ch]
        words, stack = [], [(node, prefix)]
        while stack:
            n, path = stack.pop()
            if n.is_word:
                words.append(path)
            for ch, child in n.children.items():
                stack.append((child, path + ch))
        return sorted(words)

t = Trie()
for w in ["flutter", "flame", "flask", "dart"]:
    t.insert(w)
print(t.starts_with("fl"))  # ['flame', 'flask', 'flutter']
```

**Free resources**

- [VisuAlgo: Suffix Tree, Segment Tree, Fenwick Tree](https://visualgo.net/en)
- [Competitive Programmer's Handbook (free PDF)](https://cses.fi/book/book.pdf) — greedy, bits, trees and advanced structures
- [CP-Algorithms](https://cp-algorithms.com/) — segment tree, Fenwick tree, KMP, MST
- [NeetCode roadmap: Greedy, Intervals, Tries, Bit Manipulation](https://neetcode.io/roadmap)

**Practice (in order)**

| #   | Problem                                                                                                                 | Topic               | Level  |
| --- | ----------------------------------------------------------------------------------------------------------------------- | ------------------- | ------ |
| 1   | [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)                                                     | Bits                | Easy   |
| 2   | [Single Number](https://leetcode.com/problems/single-number/)                                                           | XOR                 | Easy   |
| 3   | [Jump Game](https://leetcode.com/problems/jump-game/)                                                                   | Greedy              | Medium |
| 4   | [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)                                   | Intervals           | Medium |
| 5   | [Gas Station](https://leetcode.com/problems/gas-station/)                                                               | Greedy              | Medium |
| 6   | [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)                               | Trie                | Medium |
| 7   | [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/) | Trie + DFS          | Medium |
| 8   | [Word Search II](https://leetcode.com/problems/word-search-ii/)                                                         | Trie + backtracking | Hard   |

## Free resource library

Pick one main video source and one practice list, and stick with them; jumping between ten resources is the most common reason people stall.

| Resource                                                                                                          | Type                  | Use it for                                                |
| ----------------------------------------------------------------------------------------------------------------- | --------------------- | --------------------------------------------------------- |
| [NeetCode Roadmap](https://neetcode.io/roadmap)                                                                   | Problem list + videos | Main practice track; the NeetCode 150 maps to Phases 1–10 |
| [Abdul Bari (YouTube)](https://www.youtube.com/@abdul_bari)                                                       | Video lectures        | Clear whiteboard explanations of theory                   |
| [freeCodeCamp (YouTube)](https://www.youtube.com/@freecodecamp)                                                   | Full-length courses   | Multi-hour DSA and DP courses in one sitting              |
| [MIT 6.006 Introduction to Algorithms](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) | University course     | Deeper theory, lecture notes and problem sets             |
| [Princeton Algorithms, Part I (Coursera)](https://www.coursera.org/learn/algorithms-part1)                        | University course     | Free to audit; strong on sorting, trees and union-find    |
| [VisuAlgo](https://visualgo.net/en)                                                                               | Visualizer            | Animated view of every structure in this roadmap          |
| [Python Tutor](https://pythontutor.com/)                                                                          | Visualizer            | Step through your own code and see pointers and recursion |
| [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)                                                              | Reference             | Quick complexity lookups                                  |
| [Open Data Structures](https://opendatastructures.org/)                                                           | Free book             | Implementations of lists, trees, heaps and hash tables    |
| [Jeff Erickson: Algorithms](https://jeffe.cs.illinois.edu/teaching/algorithms/)                                   | Free book             | Recursion, backtracking, DP and graphs in depth           |
| [Competitive Programmer's Handbook](https://cses.fi/book/book.pdf)                                                | Free book             | Compact guide to algorithms, pairs with CSES              |
| [CP-Algorithms](https://cp-algorithms.com/)                                                                       | Reference site        | Exact implementations of advanced algorithms              |
| [Red Blob Games](https://www.redblobgames.com/)                                                                   | Interactive articles  | Graphs, grids and pathfinding for game developers         |
| [LeetCode Patterns](https://seanprashad.com/leetcode-patterns/)                                                   | Problem list          | Problems tagged by pattern for focused practice           |
| [Tech Interview Handbook](https://www.techinterviewhandbook.org/)                                                 | Guide                 | Study plans and interview tips once you finish            |
| [CSES Problem Set](https://cses.fi/problemset/)                                                                   | Problems              | Harder practice after the main track                      |

Links are from knowledge as of mid-2026 and were not checked live; if one has moved, search the resource name.

## 16-week schedule and progress checklist

The full track takes 16 weeks at 1–2 hours a day, about 85 problems in total. Tick each box as you finish it; move on when you can solve a phase's easy problems unaided.

**A typical study day (90 minutes)**

1. 20 minutes: watch or read today's concept.
2. 15 minutes: build the structure or example from scratch.
3. 45 minutes: solve 1–2 new problems.
4. 10 minutes: re-solve one problem from 2 days or 1 week ago.

**Checklist**

- [ ] Week 1 — Phase 0: Big-O, 3 warm-up problems
- [ ] Weeks 2–3 — Phase 1: arrays and strings, 9 problems
- [ ] Week 4 — Phase 2: hashing, build MyHashMap, 7 problems
- [ ] Weeks 5–6 — Phase 3: linked lists, stacks, queues, 9 problems
- [ ] Week 7 — Phase 4: recursion and backtracking, 7 problems
- [ ] Week 8 — Phase 5: sorting and binary search, write merge sort, 7 problems
- [ ] Weeks 9–10 — Phase 6: trees and BSTs, 8 problems
- [ ] Week 11 — Phase 7: heaps, 7 problems
- [ ] Weeks 12–13 — Phase 8: graphs, all 4 algorithms from scratch, 9 problems
- [ ] Weeks 14–15 — Phase 9: dynamic programming, 9 problems
- [ ] Week 16 — Phase 10: greedy, tries, bits, 8 problems
- [ ] After week 16 — finish the remaining [NeetCode 150](https://neetcode.io/practice) problems, then start CSES or weekly LeetCode contests

**Signs you are ready to move on**

- You can explain the phase's structure to a friend without notes.
- You can write its hands-on examples from memory.
- You solve most of its medium problems within 30 minutes.
