---
module: 		Epitech Documentation
title: 			Unit Tests for Haskell
subtitle: 	How to write them

author: 		Arthur Soulie
version: 		1.0

noFormalities: 		true
---

#newpage

# Prerequisites

Contrary to C, you are ***free to use any testing library*** (or even write your own). However we recommand using [HUnit](https://hackage.haskell.org/package/HUnit) or [Hspec](https://hspec.github.io/).
The only requirement for haskell unit tests in your project tree is that the files containing the unit tests must be placed in a folder named `test` at the root of the project.

#hint(The subtree of this `test` directory is up to you. The only exception is the `test/coverage` folder that we will use to collect coverage informations.)

#hint(Ever heard of [QuickCheck](https://hackage.haskell.org/package/QuickCheck) ?)

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
- Place your `.tix` coverage files in the `test/coverage` folder.

When running the `tests_run` rule of your Makefile you should now see the tests being executed and the coverage be displayed.
Equally important, you should now have some `.tix` files in your `test/coverage` directory. This is the directory that will be checked when evaluating your coverage.

Here is a quick command to export your coverage file. Don't worry, it's on me!
#terminal(stack hpc report --all --destdir ${TESTDIR})

