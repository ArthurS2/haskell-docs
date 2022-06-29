---
module: 		Epitech Documentation
title: 			Haskell Coding Style
subtitle: 		Keep your functional code nice and clean

author: 		Marc Planard
version: 		1.0

noFormalities: 		true
---

The *Epitech Haskell Coding Style* is a set of rules, guidelines and programming conventions that has been created within the school, and that you have to respect. #br

It applies to all the source files present in your projet, with the notable
exception of the **test/**, **tests/** and **bonus/** directories. #br

It is compulsory on all programs written in Haskell as part of Epitech projects, regardless of the year or unit.

#hint(It's easier and quicker to follow the guide style from the beginning of a project rather than to adapt an existing code at the end.)

***

The goal of this *Coding Style* is to prevent the usage of common anti-patterns and to encourage students to write idiomatic haskell. #br

Its philosophy is to write code in a **declarative** style as much as possible, avoiding patterns remembering imperative constructs.

***

There are 3 levels of severity: **major** ![major](images/major.png), **minor** ![minor](images/minor.png) and **info** ![info](images/info.png). #br

There are many and many ways to produce unclean code.
Even though one cannot mention all of them in this document, they have to be respected. 
We call them **implicit rules** when not explicitly defined in this document.

#warn(Implicit rules are considered as infos ![info](images/info.png).)

***

#hint(This document is inspired by [Haskell's Wiki Programming Guidelines](https://wiki.haskell.org/Programming_guidelines)\, which you should read too.)


#newpage

# O- Files organization

## O1- Contents of the delivery folder

![major](images/major.png) Your delivery folder should contain only **files required for compilation**.

#hint(This means no compiled(`.o`\, `.hi`\, `.a`\, `.so`\, ...)\, temporary or unnecessary files (`*~`\ `* #`\, `*.d`\, `toto`\,...).)

## O2- File extension

![major](images/major.png) Sources in a Haskell program should only have extension **`.hs`**.


## O3- File coherence

![major](images/major.png) A Haskell project must be organised in **modules**, each of which should match a **logical entity**, and group all the functions and data structures associated with that entity.

#hint(There is no limit to the number of functions in a single file)

## O4- Naming files and folders

![major](images/major.png) The name of a file should match the name of its module. Therefore, files and modules must be named in **UpperCamelCase** and in English.

#hint(It is tolerated for the file containing the main to be named after the project's executable, in lower-case.)

#newpage

# E- Extensions

## E1- Language Extensions

![major](images/major.png) All languages extensions are forbidden.

# T- Types

# T1- Top level bindings signatures

![major](images/major.png) All top level bindings must have an accompanying type signature.

```haskell

-- T1 violation
main = putStrLn "hello world"

-- No T1 violation
main :: IO ()
main = putStrLn "hello world"
```

# M- Mutability

# M1- Mutable variables

![major](images/major.png) Mutable variables are strictly forbidden.

#hint(This forbids the use of all types allowing mutation, such as 
 **Data.IORef**, **Data.STRef** or **Control.Concurrent.STM.TVar** but not **Control.Monad.Trans.State**)

# F- Functions

## F1- Coherence of functions

![minor](images/minor.png) A function should only do **one thing**, not mix the different levels of abstraction and respect the [principle of single responsibility](https://en.wikipedia.org/wiki/Single_responsibility_principle) (a function must only be changed for one reason). #br

A function should be less than 10 lines long and 80 columns wide.

## F2- Naming functions

![minor](images/minor.png) The name of a function should **define the task it executes** and should **contain a verb**.

#hint(For example\, the `voyalsNb` and `dijkstra` functions are incorrectly named. `getVoyalsNumber` and `searchShortestPath` are more meaningful and precise.)

All function names should be in English, according to the `lowerCamelCase` convention. Special characters are tolerated as long as they are justified and used sparingly. 

#hint(Abbreviations are tolerated if they significantly reduce the name without losing meaning.)

#newpage 

# V- Variables

## V1- Naming identifiers

![minor](images/minor.png) All identifier names should be **in English**, according to the **`lowerCamelCase` convention**

#hint(Abbreviations are tolerated as long as they significantly reduce the name length without losing meaning, or if they are idiosyncratic to Haskell \(for example: **x:xs**\))

The type names and constructors should be **in English**, according to the **`UpperCamelCase` convention**. 



# C- Control structure

Unless otherwise specified, all control structures are **allowed**.

## C1- Conditional branching

![major](images/major.png) Nested **If** statements are stricly forbidden.

```haskell
-- C1 violation
foo :: Int -> Int -> Int
foo a b = if a == 0
          then b
          else if b > 0
               then a-b
               else b-a
           
-- No C1 violation
foo :: Int -> Int -> Int
foo 0 b = b
foo a b | b > 0 = a-b
        | otherwise = b-a
```

## C2- Guards and pattern matching

![major](images/major.png) Guards which can be expressed as pattern matchings must be expressed as such.

```haskell
-- C2 violation
foo :: [Int] -> Int
foo lst | lst == [] = 0
        | head lst == 1 = 1

-- No C2 violation
foo :: [Int] -> Int
foo [] = 0
foo (1:_) = 1
```


## D- Do notation

Unjustified use of the do notation is forbidden.

## D1- Useless do

![major](images/major.png) The **Do** notation is forbidden unless it contains a generator (a statement with a left arrow).

```haskell
-- D1 violation
foo :: Int -> Int -> Int
foo x y = do
  let x2 = x * x
  let y2 = y * y
  sqrt $ x + y
  
-- No D1 violation
foo :: Int -> Int -> Int
foo x y = let x2 = x * x
              y2 = y * y
          in sqrt (x + y)
```

```haskell
-- No D1 violation
printLineLength :: IO ()
printLineLength = do
  line <- getLine
  print $ length line
```

For simple chaining of actions, use the **>>** operator:

```haskell
-- D1 violation
printUsage :: IO ()
printUsage = do
    putStrLn "usage: foo [options] [files]"
    putStrLn "       -s : simple"
    putStrLn "       -h : hard"
    
-- No D1 violation
printUsage :: IO ()
printUsage = putStrLn "usage: foo [options] [files]" >>
             putStrLn "       -s : simple" >>
             putStrLn "       -h : hard"
```
#warn(To prevent any circumvention of rule D1, useless generators are forbidden \(for example: x <- return 42 is an implicit D1 violation\))
