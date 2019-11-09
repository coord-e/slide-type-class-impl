## Implement and Understand Type Classes

---

## About me

![icon](icon.png)

- @coord_e
- Coding in Haskell for ~1y

---

### Type Classes - Introduction (1/2)

```haskell
-- simplified!
class Num a where
  mul :: a -> a -> a
```

---

### Type Classes - Introduction (2/2)

```haskell
mulInt :: Int -> Int -> Bool
mulFloat :: Int -> Int -> Bool

square :: Num a => a -> a
square x = mul x x


instance Num Int where
  mul = mulInt

instance Num Float where
  mul = mulFloat
  
main = print (square 3.0 2.0)
-- => 6.0
```

---

### Essense of Type Classes

- Same name for different implementation
- Dispatched depending on its type
- "ad-hoc polymorphism"

---

### Inspection (1/3)

"Type Constraint"

```haskell
> :k Num
Num :: * -> Constraint

> :k Num Int
Num Int :: Constraint
```

---

### Inspection (2/3)

type constraint disappears when typed

```haskell
> :t mul
mul :: Num a => a -> a -> a

> :t mul :: Int -> Int -> Int
mul :: Int -> Int -> Int :: Int -> Int -> Int

> :t square
square :: Num a => a -> a

> :t square (1 :: Int)
square (1 :: Int) :: Int
```

---

### Inspection (3/3)

...or not

```haskell
> :t square 'a'
...
• No instance for (Num Char) arising from a use of ‘square’
...
```

---

### To-do?

- Introduce type constractor with kind "* -> Constraint" in class declaration
- Introduce "Type Constraint" for
  * overloaded name, and
  * functions which contrain constrainted name appears in it
- Resolve "Type Constraint" when
  * suitable instance is found

---

### Questions

- How can we replace names with suitable implementation?
  * overloaded names, just obtain it from instance declaration
  * what if it is an ordinally function with type constraint?
  
---

### Solution

**Dictionary-passing**

```haskell
square x = mul x x
main = print $ square 1
-- is translated to
square' mul x = mul x x
main = print $ square' mulInt 1
```

---

### Here a paper comes...

- Wadler, Philip, and Stephen Blott. "How to make ad-hoc polymorphism less ad hoc." Proceedings of the 16th ACM SIGPLAN-SIGACT symposium on Principles of programming languages. ACM, 1989.

---

### 
