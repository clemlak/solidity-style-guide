# Solidity Style Guide

## Introduction

This is my personal attempt to write a cool style guide for [Solidity](https://soliditylang.org/), all the recommendations that you will read in this guide are purely personal and opinionated, have fun reading!

## Imports

### Always use named imports

Using named imports is cleaner and helps quickly figuring out where imports come from.

```solidity
// This is bad
import "Foo.sol";

// This is good
import { IFoo } from "Fool.sol";
```
