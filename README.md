```haskell
addMe :: Integer -> Integer -> Integer
addMe x y = (+) x y

main :: IO ()
main =  do
  putStr "Sum of x + y = "
  print(addMe 10 25)
```
ZADANIE 1 ^

```haskell
square::Integer -> Integer
square x = x * x

cube::Integer -> Integer
cube x = x * x * x

average::Integer -> Integer -> Double
average x y = fromIntegral(x + y)/2

main :: IO ()
main =  do
  putStr "Square of x = "
  print(square 5)
  putStr "Cube of x = "
  print(cube 5)
  putStr "Average of square and cube of x = "
  print(average (square 5) (cube 5))
```
ZADANIE 2 ^

```haskell 
squareFunction::Float -> Float -> Float -> (Float, Float)
squareFunction a b c = 
  let delta = b * b - 4 * a * c
  in if delta < 0 then
      (0.0, 0.0)
    else if delta == 0 then
      let x = -b / (2 * a)
      in (x, x)
    else 
      let x1 = (-b + sqrt delta) / (2 * a)
          x2 = (-b - sqrt delta) / (2 * a)
          in (x1, x2)
        
        
main::IO()
main = do
  putStr "Delta = "
  print(squareFunction 1 (-3) 2)
```
ZADANIE 3a ^

```haskell
squareFunction :: Float -> Float -> Float -> (Float, Float)
squareFunction a b c
  | delta < 0  = (0.0, 0.0)
  | delta == 0 = (x, x)
  | otherwise  = (x1, x2)
  where
    delta = b * b - 4 * a * c
    x  = -b / (2 * a)
    x1 = (-b + sqrt delta) / (2 * a)
    x2 = (-b - sqrt delta) / (2 * a)

main::IO()
main = do
  putStr "Delta = "
  print(squareFunction 1 (-3) 2)
```
ZADANIE 3b ^

```haskell
factorial:: Integer -> Integer 
factorial 0 = 1
factorial x = x * factorial(x - 1)

main::IO()
main = do
  putStr "Silnia  = "
  print(factorial 5)
```
ZADANIE 4 ^

```haskell
fibonacci:: Integer -> Integer 
fibonacci 0 = 1
fibonacci 1 = 1
fibonacci x = fibonacci(x-1) + fibonacci(x - 2)

main::IO()
main = do
  putStr "Fibonacci  = "
  print(fibonacci 5)
```
ZADANIE 5 ^

```haskell
minmax::Integer -> Integer -> Integer -> Integer
minmax x y z =
  let mi = minimum [x,y,z]
      ma = maximum [x,y,z]
  in ma - mi

main::IO()
main = do
  putStr "MAX - MIN  = "
  print(minmax 3 1 9)
```
ZADANIE 6 ^

```haskell
sumOfSquares::Integer -> Integer -> Integer
sumOfSquares x y =
  let sqx = x * x
      sqy = y * y
  in sqx + sqy

main::IO()
main = do
  putStr "Suma kwadratów  = "
  print(sumOfSquares 3 4)
```
ZADANIE 7 ^

```haskell
lastDigit::Integer -> Integer
lastDigit x = abs x `mod` 10
 

main::IO()
main = do
  putStr "Ostatnia cyfra = "
  print(lastDigit (-17))
```
ZADANIE 8 ^

```haskell 
main :: IO ()
main = do
  let x = takeWhile (<50) (map kw [0..])
  print(x)

kw :: Integer -> Integer
kw x = x*x
```
Dlaczego to działa?
Haskell ma coś zwanego `lazy evaluation`, oznacza to mniej więcej tyle, że Haskell to leniwa dziwka i jak widzi, że nie potrzebuje całej listy to nawet jak mu wpiszemy [0..] - czyli listę, która się powinna rosszerzać w nieskończoność  - to on to pierdoli, bo widzi wcześniej takeWhile, które sprawia, że ograniczamy ilość elementów listy, które pobierzemy, więc na chuj on ma się produkować jak i tak tego nie wykorzystamy, dzięki takiemu rozwiązaniu program nie wpadnie w pętlę nieskończoną

```haskell
main :: IO ()
main = do
  let y = kw (snd ([1..],5))
  print(y)

kw :: Integer -> Integer
kw x = x*x
```
To inny przykład `lazy evaluation`, w tym przypadku mamy jeszcze ciekawszy przykład tego jak leniwy jest Haskell, mamy podaną tuple z dwoma elementami - pierwszy z nich to nieskończona tablica liczb naturalnych, drugi to... 5... i chuj. Haskell dostaje przed tuplą informacje poprzez wywołanie funkcji `snd`, która zawsze wybiera 2 element tupli - bez wyjątku. No to nasz Haskell patrzy i mówi - zaraz kurwa to na chuj ta tablica - i wiedząc, że nigdy się do niej nie dostanie, nie marnuje nawet zasobów w celu wygenerowania takiej listy.

```haskell
rev::[Int] -> [Int] 
rev [] = []
rev xs = last xs : rev (init xs)

main :: IO ()
main =  do
  putStr "List odwrócona = "
  print (rev [1, 2, 3, 4])
```
ZADANIE 3 ^

```haskell
multi::[(Int, Int, Int)]
multi = [(a,b,a*b) | a <- [1..12], b <- [1..12]]

main :: IO ()
main = print (multi)
```
ZADANIE 4 ^

```haskell
colors::[String] -> [(String, String)]
colors [] = []
colors (x:xs) = [(x,y) | y <- xs] ++ colors xs
  

main :: IO ()
main = print(colors ["red", "blue", "yellow", "green","white"])
```
ZADANIE 5 ^

```haskell
append:: [Int] -> [Int] -> [Int]
append [] ys = ys
append (x:xs) ys = x : append xs ys
  

main :: IO ()
main = print(append [1,2,3,4,5] [4,5,6,7])
```
ZADANIE 6a ^

```haskell 
member:: Int -> [Int] -> Bool
member _ [] = False 
member n (x:xs) 
  |n == x = True
  |otherwise = member n xs
  

main :: IO ()
main = print(member 3 [4,5,6,7])
```
ZADANIE 6b ^

```haskell
lastt:: [Int] -> Int
lastt [] = 0 
lastt [x] = x
lastt (_:xs) = lastt xs
  

main :: IO ()
main = print(lastt [4,5,6,7])
```
ZADANIE 6c ^

```haskell
del::Int ->  [Int] -> [Int]
del _ [] = [] 
del n (x:xs) 
  | n == x  = del n xs
  | otherwise = x : del n xs
  

main :: IO ()
main = print(del 6 [4,5,6,7])
```
ZADANIE 6d ^

```haskell
filtr::(a -> Bool) -> [a] -> [a]
filtr _ [] = []
filtr p (x:xs)
  |p x = x: filtr p xs
  |otherwise = filtr p xs
  


main::IO()
main = do 
  putStr "Filtr = "
  print(filtr (>4) [1..10])
```
ZADANIE 7 ^

```haskell
ev::[Int] -> [Int]
ev [] = []
ev (x:xs)
  |x `mod` 2 == 0 = x: ev xs
  |otherwise = ev xs
  


main::IO()
main = do 
  putStr "Równe = "
  print(ev [1..10])
```
```haskell
ev::[Int] -> [Int]
ev [] = []
ev xs = filter even xs


main::IO()
main = do 
  putStr "Równo = "
  print(ev [1..10])
```
ZADANIE 8 ^

```haskell
doubleAll::[Int] -> [Int]
doubleAll [] = []
doubleAll xs = map (*2) xs
 
  


main::IO()
main = do 
  putStr "Równe = "
  print(doubleAll [1..10])
```
ZADANIE 9 ^

```haskell
sumOfDigits :: Int -> Int
sumOfDigits n = go (abs n)
  where
    go 0 = 0
    go x = (x `mod` 10) + go (x `div` 10)



main::IO()
main = do 
  putStr "Suma = "
  print(sumOfDigits (-131))
```
ZADANIE 10 ^

```prolog
color(red, green).
color(red, blue).
color(green, red).
color(green, blue).
color(blue, red).
color(blue, green).

obok(Po, Lb, Ma, Pd, Wm) :-
  color(Po,Lb),
  color(Lb,Po),
  color(Lb,Ma),
  color(Lb,Pd),
  color(Ma, Lb),
  color(Ma,Pd),
  color(Ma, Wm),
  color(Pd, Lb),
  color(Pd, Ma),
  color(Pd, Wm),
  color(Wm, Pd),
  color(Wm, Ma).
```
ZADANIE 2 z PROLOG ^

```prolog
nwd(X,Y,Nwd) :-
  X = Y,
  Nwd = X.

nwd(X,Y,Nwd) :-
  X > Y,
  X1 is X - Y,
  nwd(X1,Y,Nwd)

nwd(X,Y,Nwd) :-
  X < Y,
  Y1 is Y - X,
  nwd(X,Y1,Nwd)
```
ZADANIE 3 z PROLOG ^


