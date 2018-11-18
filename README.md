# Ethereum Functions

This is a functional Ethereum smart contract library.

Each contract in this library will be deployed onto Ethereum's blockchain for use by other smart contracts.

Each contract in this library will abstract away some of solidity & the EVM's peculiarities, and when used together as a framework, should enable smart contracts to be more fool-proof & less error prone.

## Architecture

Each smart contract is deployed as a library and normally contains a single function.

This minimizes the gas needed for lookup of the function in the contract's code.

There be no versioning for these functions, since once it's deployed, it's final.

Contracts that use them, however, are free to store contract addresses and change them as needs change, to call different functions.

This is similar to function pointers or callbacks, as the contract address is the identifier for the code to be called.

This architecture enables function callers also to lookup the implementation of the function, since it is always (short of EVM change, I think) in a known location in the library's bytecode.

This would also enable authors of other smart contracts to validate the correctness of any algorithm they might choose to call, using automated tools, before allowing their smart contract to use them in the wild.


### Solidity rant

There are many improvements to solidity that I think should be made to align its behavior to that expected of it by most developers.

Low-level design decisions in the EVM which promote maximum flexibility, are passed along by solidity, which is a very high level language.

Because of this, developers often make assumptions about how the code should work that may not be valid, even though they make sense from a high level.

For example, operations may overflow silently without exceptions from EVM. It makes sense that they decided to go this way.

But in a high-level language like solidity, when you're calculating balances, it does not make sense to allow unsigned addition to have results smaller than the inputs.

Thus, solidity should provide these higher-level features to developers that depend on them.

Solidity should add new *_overflows types which behave the same as current types, and replace the current types with types that generate overflow-disabled code.





