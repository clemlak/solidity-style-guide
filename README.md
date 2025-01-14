# Solidity Style Guide

## Introduction

This is my personal attempt to write a cool style guide for [Solidity](https://soliditylang.org/), all the recommendations that you will read in this guide are purely personal and opinionated, have fun reading!

## Definitions

### Prefer "free definitions" when possible

Variables, functions and events can be defined outside of a `contract` or a `library`, this makes them easily accessible and reusable in other places.

### Follow naming conventions

Naming conventions for variables where defined to quickly understand what they are used for.

```solidity
// Constants should be in uppercase
uint256 constant MAX_SUPPLY = 1e25;

// Variables should be in camelCase
uint256 totalSupply = 1e24;

// Functions should be in camelCase
function totalSupply() public view returns (uint256) {
  return totalSupply;
}

// Events should be in PascalCase
event Transfer(address indexed from, address indexed to, uint256 value);

// Structs should be in PascalCase
struct Token {
  uint256 totalSupply;
}

// Enums should be in PascalCase
enum UserRole { None, Sender, Recipient }

// Modifiers should be in camelCase
modifier onlyOwner() {
  // ...
  _;
}

// Errors should be in PascalCase
error OnlyOwner();

// Interfaces should be in PascalCase
interface IRouter {
  // ...
}

// Libraries should be in PascalCase
library MathLibrary {
  // ...
}

// Contracts should be in PascalCase
contract Token {
  // ...
}
```

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

### Use error parameters to provide details

Errors might be reused multiple times in the same function, using parameters will help understand what went wrong.

```solidity
// Let's say we have users with different roles
enum UserRole { None, Sender, Recipient }

// And we revert if the user has the wrong role
error WrongUserRole(address user, UserRole expected, UserRole actual);

// This function reuses the same error twice, providing details helps understand where the error comes from
function transfer(address from, address to) public {
  require(getRole[from] == UserRole.Sender, WrongUserRole(from, UserRole.Sender, getRole[from]));
  require(getRole[to] == UserRole.Recipient, WrongUserRole(to, UserRole.Recipient, getRole[to]));
}
```

## Comments

### Use NatSpec

Use `///` for single line comments, and `/** ... */` for multi-line comments.

```solidity
/// @notice This is a single line comment

/**
 * @notice This is a multi-line comment, you can write
 * as much as you want here.
 */
```
