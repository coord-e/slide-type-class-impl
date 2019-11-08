## Implement and Understand Type Classes

---

## About me

![icon](icon.png)

- @coord_e
- Coding in Haskell for ~1y

---

### Type Classes - Introduction (1/2)

```haskell
class Num a where
  add :: a -> a -> a
  mul :: a -> a -> a
```

---

### Type Classes - Introduction (2/2)

```haskell
addInt, mulInt :: Int -> Int -> Bool
addFloat, mulFloat :: Int -> Int -> Bool

square :: Eq a => a -> a
square x = mul x x


instance Eq Int where
  add = addInt
  mul = mulInt

instance Eq Float where
  add = addFloat
  mul = mulFloat
  
main = print (square 3.0 2.0)
-- => 6.0
```

---

### Inspection (1/3)

"Type Constraint"

```haskell
> :k Num
Num :: * -> Constraint
> :k Num Int
Num Int :: Constraint
```

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

### Inspection (3/3)

...or not

```haskell
> :t square 'a'
...
• No instance for (Num Char) arising from a use of ‘square’
...
```

### To-do?

- Introduce "Type Constraint" for
  * overloaded name, and
  * functions which contrain constrainted name appears in it
- Resolve "Type Constraint" when
  * suitable instance is found
