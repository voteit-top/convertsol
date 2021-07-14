## Welcome to Convert.sol

That would be perfect if you needn't any type conversion while developing Solidity. but fact is you will have to convert one to another somewhile and you will find that is not easy to do that in Solidity.

### Useful conversions
## from string to uint
if convert decimal number, eg: from '123' to 123, let's see what you need do:
1. you need convert string to bytes,since string cannot be iterated.
2. iterate bytes and map ascii byte to decimal number and accumulate them like:
```
1*100 + 2*10 + 3.
```
if convert hex number, eg:from '0x123' to 291 , let's see what you need do:
1. you need convert string to bytes,since string cannot be iterated.
2. recognize hex tag: '0x'
3. iterate bytes and map ascii byte to hex digit and calculate like:
```
1<<4*2 + 2<< 4*1 + 3 << 4*0  
```
### ASCII to uint
for '123' as example, when it was converted to bytes, it will look like: 0x313233, so we need map each byte to digit.
also, for hex number, from a to f and their upper case, should be convert to 10-15.
```
    function asciiToUint(bytes1 b) internal pure returns(uint8)
    {
        if(b >= 0x30 && b <= 0x39)
            return uint8(b&0x0F);
        else if((b >= 0x41 && b <= 0x46) || (b >= 0x61 && b <= 0x66))
            return 9 + uint8(b&0x0F);     
    }
```
so, complete code:
```
    function stringToUint(bytes memory b) internal pure returns (uint)
    {
        uint out=0;
        uint offset = 0;
        bool isHex = false;
        uint len = b.length;
        if(len == 0)
            return out;
        if(len > 1 && b[0] == bytes1(0x30) && (b[1] == bytes1(0x58)||b[1] == bytes1(0x78)))
        {
            isHex = true;
            offset = 2;
        }    
        for(uint i=offset;i<len;i++)
        {            
            uint bu = asciiToUint(b[i]);
            if(isHex)
                out |= (bu << (4*(len-i-1)));
            else
                out += (bu*(10**(len-i-1)));
        }                
        return out;
    }
```
Note: exceptional case is not considered, eg:12-sdf123 or 0xsdfk123 

## from string to int
## from bytes to uint
## from bytes to int
## from bytes to bytes32
