# Implement and Understand Type Classes

## About me

![icon](icon.png)

- @coord_e
- Coding in Haskell for ~1y

## Type Classes - Introduction (1/2)

```haskell
class Num a where
  add :: a -> a -> a
  mul :: a -> a -> a
```

## Type Classes - Introduction (2/2)

```haskell
addInt, mulInt :: Int -> Int -> Bool
addFloat, mulFloat :: Int -> Int -> Bool

square :: Eq a => a -> a -> a
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
