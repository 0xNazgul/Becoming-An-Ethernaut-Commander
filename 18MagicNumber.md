# Magic Number

**HINT:** This one is pretty tricky and goes into the deconstruction of contracts, bytes and opcode. Your going to want to review the [ETHEREUM: A SECURE DECENTRALISED GENERALISED TRANSACTION LEDGER: yellow paper] (http://gavwood.com/paper.pdf) page 22. 

<details>
<summary>Part 1</summary>
Looking through the yellow paper, your going to want 2 things the runtime opcodes and the initialization opcodes
to start with the runtime opcodes will go like so:

* We will use mstore in the contract so will have 2 parameters to it
    * v is the value
    * p is the memory slot 
* 6042 
    * v: PUSH1 0x42
* 6000
    * p: PUSH1 0x0
* 52
    * this is mstore
* Now return this by with the parameters:
    * s the size
    * p the slot
* 6020
    * s: PUSH1 is 32 bytes
* 6000
    * p: PUSH1 stored in slot 0x0
* f3
    * return

* So far we have: ```604260005260206000f3``` 
* The length of this is 0x0a or 10 which is what we need

</details>

<details>
<summary>Part 2</summary>
<p>
For the initialization opcodes, the EVM will handle this part so all we have to do is offset the runtime opcodes like below:

```
0x00000000000000000000000000000000000000000000604260005260206000f3 (length 0x20 or 32) 
                                              ^ (offset 0x16 or 22)
```                                              
Then make the contract:

```
pragma solidity ^0.6.0;

contract MagicNumSolver {
  constructor() public {
    assembly {
      mstore(0, 0x602a60005260206000f3)
      return(0x16, 0x0a)
    }
  }
}
```

</p>
</details>

<details>
<summary>Part 3</summary>
<p>
All that's left is to copy the contract address and go to the console:

```js
await contract.setSolver("Your_Deployed_Contract")
```

</p>
</details>