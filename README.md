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

### Highlight module imports using a special character

Module imports can be highlighted using a special character, this makes it easier to distinguish them from other imports.

```solidity
import { IFoo } from "@foo/IFool.sol";
```

### Use absolute paths for imports

Relative paths require some brain power to figure out where the file is located, using absolute paths is cleaner and easier to understand.

```solidity
// This is bad
import { IFoo } from "../../interfaces/IFoo.sol";

// This is good
import { IFoo } from "src/interfaces/IFoo.sol";
```

### Order imports

Imports should be ordered in the following way:

1. Modules or libraries (external packages)
2. Local files

```solidity
import { IFoo } from "@foo/IFoo.sol";
import { IBar } from "src/interfaces/IBar.sol";
```

## Errors

### Use custom revert errors with require

`require` now accepts custom revert errors, this is a great improvement as strings are expensive to store onchain.

```solidity
// This is bad
require(msg.sender == owner, "Only owner can call this function");

// This is good
require(msg.sender == owner, OnlyOwner());
```

### Use explicit error names

Error names should be clear enough to explain what went wrong.

```solidity
// This is bad
error WrongAddress();

// This is good
error OnlyOwner();
```
