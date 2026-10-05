# 1. What is Big-O?

Big-O describes **how the amount of work an algorithm does grows as the input gets larger**.

The important word is **grows**.

Suppose you have:

```dart
List<int> numbers = [10, 20, 30, 40, 50];
```

If I ask:

> "Does this list contain 40?"

You could check:

```dart
for (final number in numbers) {
  if (number == 40) {
    return true;
  }
}
```

For 5 items, maybe you check 4 items.

For 100 items, you might check 100.

For 1,000,000 items, you might check 1,000,000.

So the work grows roughly with `n`.

That's:

**O(n)**

where `n` = number of input elements.

---

# 2. Why do we need Big-O?

Imagine two algorithms.

### Algorithm A

```text
100 items   → 100 operations
1,000 items → 1,000 operations
1,000,000   → 1,000,000 operations
```

### Algorithm B

```text
100 items   → 10,000 operations
1,000 items → 1,000,000 operations
1,000,000   → 1,000,000,000,000 operations
```

Both might work perfectly with small data.

But when your data becomes large, Algorithm B becomes disastrous.

Big-O helps us answer:

> **"How will this algorithm behave when the input becomes huge?"**

---

# 3. The most important Big-O complexities

You should know these first:

| Big-O          | Name         | General behavior    |
| -------------- | ------------ | ------------------- |
| **O(1)**       | Constant     | Excellent           |
| **O(log n)**   | Logarithmic  | Excellent           |
| **O(n)**       | Linear       | Good                |
| **O(n log n)** | Linearithmic | Usually good        |
| **O(n²)**      | Quadratic    | Can become slow     |
| **O(2ⁿ)**      | Exponential  | Very expensive      |
| **O(n!)**      | Factorial    | Extremely expensive |

Visually:

genui{"learning_viz":{"type_id":"BIG_O_TIME_COMPLEXITY","locale_override":"en-US"}}

Don't memorize the graph yet. We'll **derive these ourselves**.

---

# 4. O(1) — Constant Time

This is the easiest.

```dart
int first(List<int> numbers) {
  return numbers[0];
}
```

Whether the list contains:

```text
10 items
100 items
1,000 items
1,000,000 items
```

we only access one element.

Therefore:

```text
O(1)
```

### Another example

```dart
final user = users[10];
```

The list size doesn't fundamentally change the number of operations.

### Important misconception

O(1) does **not** mean:

> "It takes exactly 1 operation."

It means:

> **The amount of work does not grow with n.**

For example:

```dart
void doSomething() {
  print("A");
  print("B");
  print("C");
  print("D");
  print("E");
}
```

That's still:

```text
O(1)
```

because 5 operations are still a constant.

---

# 5. O(n) — Linear Time

Now let's look at the classic:

```dart
bool contains(List<int> numbers, int target) {
  for (final number in numbers) {
    if (number == target) {
      return true;
    }
  }

  return false;
}
```

Suppose:

```text
n = 5
```

Worst case:

```text
5 operations
```

If:

```text
n = 100
```

Worst case:

```text
100 operations
```

If:

```text
n = 1,000,000
```

Worst case:

```text
1,000,000 operations
```

Therefore:

```text
O(n)
```

---

# 6. Let's make this more interesting

Consider:

```dart
void printNumbers(List<int> numbers) {
  for (final number in numbers) {
    print(number);
  }

  for (final number in numbers) {
    print(number);
  }
}
```

You might say:

```text
O(n) + O(n)
```

which is:

```text
O(2n)
```

But Big-O drops constants:

```text
O(n)
```

### Why?

Because we're interested in **growth**.

For huge `n`:

```text
2n
```

and

```text
n
```

have the same growth category.

---

# 7. O(n²) — Quadratic

Now things get interesting.

Look at this:

```dart
void printPairs(List<int> numbers) {
  for (final a in numbers) {
    for (final b in numbers) {
      print('$a $b');
    }
  }
}
```

We have:

```text
loop
  └── loop
```

If:

```text
n = 5
```

the inner loop runs 5 times for every outer iteration.

So:

```text
5 × 5 = 25
```

If:

```text
n = 100
```

then:

```text
100 × 100 = 10,000
```

If:

```text
n = 1,000
```

then:

```text
1,000 × 1,000
= 1,000,000
```

Therefore:

```text
O(n²)
```

---

# 8. The easiest rule for recognizing Big-O

When you see nested loops:

```dart
for (...) {
  for (...) {
  }
}
```

think:

```text
O(n²)
```

Three nested loops:

```dart
for (...) {
  for (...) {
    for (...) {
    }
  }
}
```

usually means:

```text
O(n³)
```

Four:

```text
O(n⁴)
```

etc.

But **don't blindly count loops**. We'll get to why later.

---

# 9. O(log n)

This one is extremely important.

Consider **binary search**.

Imagine you have:

```text
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
```

I ask:

> Find 13.

Instead of checking:

```text
1
2
3
4
...
```

Binary search checks the middle.

```text
1 2 3 4 5 6 7 [8] 9 10 11 12 13 14 15
```

13 is bigger than 8.

So eliminate half:

```text
9 10 11 12 [13] 14 15
```

Again:

```text
13 14 15
```

Again:

```text
13
```

We repeatedly cut the problem in half.

That's:

```text
O(log n)
```

---

# 10. Why is log n so good?

Suppose you have:

```text
n = 1,000,000
```

Binary search doesn't need one million checks.

Roughly:

```text
log₂(1,000,000) ≈ 20
```

Only around **20 divisions by two**.

That's why algorithms such as binary search are extremely powerful.

---

# 11. O(n log n)

You'll see this everywhere in real software.

Many efficient sorting algorithms are:

```text
O(n log n)
```

For example, merge sort.

Conceptually:

```text
[8, 3, 5, 1, 9, 2, 7, 4]
```

Split:

```text
[8,3,5,1] [9,2,7,4]
```

Split again:

```text
[8,3] [5,1] [9,2] [7,4]
```

Eventually:

```text
[8] [3] [5] [1] [9] [2] [7] [4]
```

Then merge them back in sorted order.

There are roughly:

```text
log n
```

levels.

At each level, you process:

```text
n
```

elements.

Therefore:

```text
n × log n

= O(n log n)
```

---

# 12. O(2ⁿ) — Exponential

Now things become dangerous.

Imagine:

```dart
void generate(int n) {
  if (n == 0) return;

  generate(n - 1);
  generate(n - 1);
}
```

Each call creates **two more calls**.

Conceptually:

```text
             n
           /   \
        n-1     n-1
       /  \     /  \
     n-2 n-2  n-2 n-2
```

The number of calls grows roughly:

```text
2ⁿ
```

Therefore:

```text
O(2ⁿ)
```

This becomes huge extremely quickly.

For example:

```text
2¹⁰  = 1,024
2²⁰  = 1,048,576
2³⁰  = 1,073,741,824
```

That's why naive recursive solutions can become unusable.

---

# 13. O(n!) — Even worse

Factorial:

```text
n!
```

means:

```text
n × (n-1) × (n-2) × ... × 1
```

For example:

```text
5! = 120
```

But:

```text
10! = 3,628,800
```

and:

```text
20! = 2,432,902,008,176,640,000
```

This appears in problems involving permutations.

For example:

> "Try every possible ordering of these cities."

If there are `n` cities:

```text
n!
```

possible orderings.

That's why brute-force permutation algorithms become impossible very quickly.

---

# 14. The Big-O hierarchy

Generally, from better to worse:

```text
O(1)
   ↓
O(log n)
   ↓
O(n)
   ↓
O(n log n)
   ↓
O(n²)
   ↓
O(n³)
   ↓
O(2ⁿ)
   ↓
O(n!)
```

For large inputs, you generally want to move **up this list as little as possible**.

---

# 15. Let's analyze real Dart code

Now we'll start doing actual exercises.

Consider:

```dart
int sum(List<int> numbers) {
  int total = 0;

  for (final number in numbers) {
    total += number;
  }

  return total;
}
```

How many times does the loop run?

```text
n
```

Therefore:

```text
O(n)
```

---

# 16. Example 2

```dart
int getFirstAndLast(List<int> numbers) {
  final first = numbers.first;
  final last = numbers.last;

  return first + last;
}
```

Operations don't depend on list size.

Therefore:

```text
O(1)
```

---

# 17. Example 3

```dart
void printPairs(List<int> numbers) {
  for (final a in numbers) {
    for (final b in numbers) {
      print('$a $b');
    }
  }
}
```

First loop:

```text
n
```

Second loop:

```text
n
```

Multiply:

```text
n × n
```

Therefore:

```text
O(n²)
```

---

# 18. Example 4 — Don't automatically say O(n²)

Look carefully:

```dart
void example(List<int> numbers) {
  for (final number in numbers) {
    print(number);
  }

  for (final number in numbers) {
    print(number);
  }
}
```

These loops are **not nested**.

They're sequential.

So:

```text
O(n) + O(n)
```

=

```text
O(2n)
```

Drop the constant:

```text
O(n)
```

This is a very important Big-O rule.

---

# 19. Example 5 — Different input sizes

Consider:

```dart
void example(List<int> a, List<int> b) {
  for (final x in a) {
    print(x);
  }

  for (final y in b) {
    print(y);
  }
}
```

Don't say:

```text
O(n²)
```

because we have two loops.

We actually have:

```text
O(a + b)
```

because the lists can have different sizes.

This is an important real-world complexity analysis technique.

---

# 20. Example 6 — Nested but different inputs

```dart
void example(List<int> a, List<int> b) {
  for (final x in a) {
    for (final y in b) {
      print('$x $y');
    }
  }
}
```

Now:

```text
a × b
```

Therefore:

```text
O(a × b)
```

Not necessarily:

```text
O(n²)
```

unless `a` and `b` are approximately the same size.

---

# 21. Constants disappear

Suppose:

```dart
void example(List<int> numbers) {
  for (final n in numbers) {
    print(n);
  }

  for (final n in numbers) {
    print(n);
  }

  for (final n in numbers) {
    print(n);
  }
}
```

Technically:

```text
O(3n)
```

Big-O:

```text
O(n)
```

Similarly:

```text
O(500n)
```

is still:

```text
O(n)
```

Because Big-O focuses on asymptotic growth.

---

# 22. Smaller terms disappear

Suppose your algorithm does:

```text
n² + n + 10
```

Big-O is:

```text
O(n²)
```

Why?

Because as `n` becomes enormous:

```text
n²
```

dominates:

```text
n
```

and:

```text
10
```

So:

```text
O(n² + n + 10)
```

becomes:

```text
O(n²)
```

---

# 23. Let's practice simplifying

### Question 1

```text
3n + 10
```

Answer:

```text
O(n)
```

---

### Question 2

```text
5n² + 10n + 100
```

Answer:

```text
O(n²)
```

---

### Question 3

```text
n³ + n² + n
```

Answer:

```text
O(n³)
```

---

### Question 4

```text
n + log n
```

Answer:

```text
O(n)
```

because:

```text
n
```

grows faster than:

```text
log n
```

---

# 24. A very important real-world example

Imagine your Flutter app has:

```dart
List<Customer> customers;
List<Ticket> tickets;
```

You want to find tickets belonging to each customer.

A beginner might write:

```dart
for (final customer in customers) {
  for (final ticket in tickets) {
    if (ticket.customerId == customer.id) {
      // ...
    }
  }
}
```

If:

```text
customers = 10,000
tickets = 100,000
```

you're potentially doing:

```text
10,000 × 100,000

= 1,000,000,000
```

comparisons.

That's:

```text
O(customers × tickets)
```

or approximately:

```text
O(n²)
```

if both are similar in size.

---

# 25. We can improve it

Create a lookup map:

```dart
final ticketsByCustomer = <int, List<Ticket>>{};

for (final ticket in tickets) {
  ticketsByCustomer
      .putIfAbsent(ticket.customerId, () => [])
      .add(ticket);
}
```

Building the map:

```text
O(tickets)
```

Then:

```dart
final customerTickets = ticketsByCustomer[customer.id];
```

Map lookup is approximately:

```text
O(1)
```

on average.

So instead of:

```text
O(customers × tickets)
```

we can get something closer to:

```text
O(customers + tickets)
```

That's a **huge practical improvement**.

---

# 26. This is where Big-O becomes useful for Flutter

Suppose your Flutter screen has:

```dart
ListView.builder(
  itemCount: customers.length,
  itemBuilder: (_, index) {
    final customer = customers[index];

    final tickets = allTickets
        .where((ticket) => ticket.customerId == customer.id)
        .toList();

    return CustomerCard(
      customer: customer,
      tickets: tickets,
    );
  },
);
```

If `where()` scans all tickets for every customer, you could accidentally create:

```text
O(customers × tickets)
```

work.

For a small dataset, nobody notices.

At scale:

```text
100 customers × 100 tickets
```

is fine.

But:

```text
10,000 customers × 100,000 tickets
```

is potentially catastrophic.

Big-O lets you see the problem **before users experience it**.

---

# 27. Big-O isn't only about time

There are actually two major things we analyze:

### Time complexity

How much computation?

```text
O(n)
O(n²)
O(log n)
```

### Space complexity

How much additional memory?

For example:

```dart
List<int> copy(List<int> numbers) {
  return [...numbers];
}
```

If the original list has `n` elements, we create another list containing `n` elements.

Therefore additional space:

```text
O(n)
```

---

# 28. Example: O(n) time and O(1) space

```dart
int sum(List<int> numbers) {
  int total = 0;

  for (final number in numbers) {
    total += number;
  }

  return total;
}
```

Time:

```text
O(n)
```

Extra space:

```text
O(1)
```

We don't create another data structure proportional to `n`.

---

# 29. Example: O(n) time and O(n) space

```dart
List<int> doubleNumbers(List<int> numbers) {
  final result = <int>[];

  for (final number in numbers) {
    result.add(number * 2);
  }

  return result;
}
```

Time:

```text
O(n)
```

Space:

```text
O(n)
```

because `result` grows with `n`.

---

# 30. The biggest mistake beginners make

They think:

> "Big-O tells me exactly how many milliseconds this function takes."

No.

This:

```text
O(n)
```

doesn't tell you:

```text
10ms
100ms
500ms
```

It describes **growth behavior**.

Two O(n) algorithms can have very different actual runtimes.

For example:

```dart
for (...) {
  // very cheap operation
}
```

versus:

```dart
for (...) {
  // expensive database/network/crypto operation
}
```

Both might technically be:

```text
O(n)
```

but their actual performance can be dramatically different.

---

# 31. Big-O vs Big-Ω vs Big-Θ

"Asymptotic notation" is actually bigger than Big-O.

There are three important notations.

## Big-O

Usually describes an **upper bound**.

```text
O(n)
```

Think:

> "It won't grow faster than this order."

---

## Big-Ω (Omega)

Lower bound.

```text
Ω(n)
```

Think:

> "It requires at least this order of work."

---

## Big-Θ (Theta)

Tight bound.

```text
Θ(n)
```

Think:

> "Its growth is actually this order."

For most programming interviews and everyday algorithm discussions, **Big-O is the notation you'll use most often**.

---

# 32. Let's do a real interview-style exercise

Analyze this:

```dart
void mystery(List<int> numbers) {
  for (final number in numbers) {
    print(number);
  }

  for (int i = 0; i < numbers.length; i++) {
    for (int j = 0; j < numbers.length; j++) {
      print(numbers[i] + numbers[j]);
    }
  }
}
```

First part:

```dart
for (final number in numbers)
```

is:

```text
O(n)
```

Second part:

```dart
for i
  for j
```

is:

```text
O(n²)
```

Together:

```text
O(n + n²)
```

Drop the smaller term:

```text
O(n²)
```

### Final answer:

```text
O(n²)
```

---

# 33. Another tricky one

```dart
void mystery(List<int> numbers) {
  for (int i = 0; i < numbers.length; i++) {
    for (int j = 0; j < 10; j++) {
      print(numbers[i]);
    }
  }
}
```

You might think:

```text
O(n²)
```

But look at the inner loop:

```dart
j < 10
```

It's always exactly 10 iterations.

So:

```text
n × 10
```

which is:

```text
O(10n)
```

Drop the constant:

```text
O(n)
```

### Answer:

```text
O(n)
```

This is a great interview trick.

---

# 34. Another important one

```dart
for (int i = 1; i < n; i *= 2) {
  print(i);
}
```

What happens?

```text
1
2
4
8
16
32
64
...
```

The value doubles every time.

How many times can you double before reaching `n`?

Approximately:

```text
log₂(n)
```

Therefore:

```text
O(log n)
```

---

# 35. Learn to recognize patterns

When you see:

### Direct access

```dart
array[index]
```

Think:

```text
O(1)
```

---

### One complete loop

```dart
for (...) {}
```

Think:

```text
O(n)
```

---

### Nested loops

```dart
for (...) {
  for (...) {}
}
```

Think:

```text
O(n²)
```

---

### Divide by 2 repeatedly

```dart
n ~/= 2;
```

Think:

```text
O(log n)
```

---

### Loop + logarithmic operation

```text
n × log n
```

Think:

```text
O(n log n)
```

---

### Two recursive branches

```text
f(n-1)
f(n-1)
```

Potentially:

```text
O(2ⁿ)
```

---

# 36. Your practical Big-O checklist

Whenever you see an algorithm, ask:

### Step 1

What is the input size?

```text
n = number of elements
```

### Step 2

How many times does each loop run?

### Step 3

Are loops sequential or nested?

Sequential:

```text
O(n) + O(n)
= O(n)
```

Nested:

```text
O(n) × O(n)
= O(n²)
```

### Step 4

Are there different input sizes?

```text
O(a + b)
```

rather than automatically:

```text
O(n)
```

### Step 5

Are there logarithmic operations?

Look for:

```text
divide by 2
double
binary search
balanced tree
```

### Step 6

Remove constants.

```text
O(5n) → O(n)
```

### Step 7

Keep the dominant term.

```text
O(n² + n) → O(n²)
```

---

# 37. Let's test your understanding

Don't look for the answers immediately.

### Problem 1

```dart
void test(List<int> numbers) {
  print(numbers[0]);
}
```

What is the complexity?

---

### Problem 2

```dart
void test(List<int> numbers) {
  for (final number in numbers) {
    print(number);
  }
}
```

---

### Problem 3

```dart
void test(List<int> numbers) {
  for (final a in numbers) {
    for (final b in numbers) {
      print(a + b);
    }
  }
}
```

---

### Problem 4

```dart
void test(List<int> numbers) {
  for (int i = 1; i < numbers.length; i *= 2) {
    print(numbers[i]);
  }
}
```

---

### Problem 5

```dart
void test(List<int> numbers) {
  for (final n in numbers) {
    print(n);
  }

  for (final n in numbers) {
    print(n);
  }
}
```

---

### Problem 6 — harder

```dart
void test(List<int> numbers) {
  for (final n in numbers) {
    for (int i = 1; i < numbers.length; i *= 2) {
      print(n + i);
    }
  }
}
```

---

### Problem 7 — harder

```dart
void test(List<int> a, List<int> b) {
  for (final x in a) {
    print(x);
  }

  for (final x in a) {
    for (final y in b) {
      print(x + y);
    }
  }
}
```

---

## Answers

Don't scroll until you've tried them.

<details>
<summary><b>Problem 1</b></summary>

```text
O(1)
```

Direct index access.

</details>

<details>
<summary><b>Problem 2</b></summary>

```text
O(n)
```

One loop over the input.

</details>

<details>
<summary><b>Problem 3</b></summary>

```text
O(n²)
```

`n × n`.

</details>

<details>
<summary><b>Problem 4</b></summary>

```text
O(log n)
```

The index doubles every iteration.

</details>

<details>
<summary><b>Problem 5</b></summary>

```text
O(n)
```

`O(n) + O(n) = O(2n) = O(n)`.

</details>

<details>
<summary><b>Problem 6</b></summary>

```text
O(n log n)
```

Outer loop:

```text
O(n)
```

Inner loop:

```text
O(log n)
```

Together:

```text
O(n log n)
```

</details>

<details>
<summary><b>Problem 7</b></summary>

```text
O(a + ab)
```

The first loop is `O(a)`.

The nested loops are `O(ab)`.

Since `ab` dominates when both inputs grow:

```text
O(ab)
```

</details>

---

# 38. The most important thing to take away

Don't try to memorize hundreds of Big-O formulas.

Instead, train yourself to **look at code and see growth**.

For example:

```dart
for (final item in items) {
```

Your brain should immediately think:

> `n`

Then:

```dart
for (final item in items) {
  for (final other in items) {
```

Your brain should think:

> `n × n = n²`

And:

```dart
for (int i = 1; i < n; i *= 2)
```

Your brain should think:

> `log n`
