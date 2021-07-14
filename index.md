## Welcome to Convert.sol

That would be perfect if you needn't any type conversion while developing Solidity. but fact is you will have to convert one to another somewhile and you will find that is not easy to do that in Solidity.

### Useful conversions
## from string to uint
if convert decimal number, eg: from '123' to 123, let's see what you need do:
1. you need convert string to bytes,since string cannot be iterated.
2. iterate bytes and map ascii byte to decimal number and multiply multiples of 10.

if convert hex number, eg:from '0x11' to 17 , let's see what you need do:
1. you need convert string to bytes,since string cannot be iterated.
2. recognize hex tag: '0x'
3. iterate bytes and map ascii byte to hex digit and shifte multiples of 4. 


## from string to int
## from bytes to uint
## from bytes to int
## from bytes to bytes32
