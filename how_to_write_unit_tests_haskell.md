---
module: 		Epitech Documentation
title: 			Unit Tests for Haskell
subtitle: 	How to write them

author: 		Arthur Soulie
version: 		1.1

noFormalities: 		true
---

#newpage

# Prerequisites

Contrary to C, you are ***free to use any testing library*** (or even write your own). However we recommand using [HUnit](https://hackage.haskell.org/package/HUnit) or [Hspec](https://hspec.github.io/).
The only requirement for your project is to have the files containing the unit tests placed in a folder named `test` at the root of the project.

#hint(The subtree of this `test` directory is up to you. The only exception is the `test/coverage` folder that we will use to collect coverage informations.)

# Running tests with stack

Using the stack build system and assuming your project is correctly configured, you should be able to run your tests with the following command:

#terminal(cd my-stack-project
#prompt stack test
)

# Evaluation at Epitech

Unless specified overwise in the project subject, your tests will be built and launched using your own Makefile.
The `Makefile` used to compile the unit tests is ***the Makefile at the root of your project directory***.


This Makefile must contains a rule named ***tests_run*** which must do three things:
- Build your unit-tests binary,
- Execute your unit-tests binary with coverage,
- Place the generated `.tix` coverage files in the `test/coverage` folder. This directory will be checked for coverage evaluation.


Here is a quick command to export your coverage file. Don't worry, it's on me!
#terminal(stack hpc report --all --destdir DESTINATION)


#hint(Ever heard of [QuickCheck](https://hackage.haskell.org/package/QuickCheck) ?)
