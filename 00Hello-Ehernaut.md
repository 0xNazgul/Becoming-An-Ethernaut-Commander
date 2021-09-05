# Hello Ethernaut

<details>
<summary> Part 1</summary>
<p>

```js
await contract.info()
```
You'll get:
```
"You will find what you need in info1()."
```
</p>
</details>

<details>
<summary> Part 2</summary>
<p>

```js
await contract.info1()
```
You'll get:
```
"Try info2(), but with \"hello\" as a parameter."
```
</p>
</details>

<details>
<summary> Part 3</summary>
<p>

```js
await contract.info2("hello")
```
You'll get:
```    
"The property infoNum holds the number of the next info method to call."
```
</p>
</details>

<details>
<summary> Part 4</summary>
<p>

```js
await contract.infoNum()
```
You'll get:
```js
    {negative: 0, words: Array(2), length: 1, red: null}
    length: 1
    negative: 0
    red: null
    words: (2) [42, empty]
```
</p>
</details>

<details>
<summary> Part 5</summary>
<p>

```js
await contract.info42()
```    
You'll get:
```
"theMethodName is the name of the next method."
```
</p>
</details>

<details>
<summary> Part 6</summary>
<p>

```js
await contract.theMethodName()
```
You'll get:
```
"The method name is method7123949."
```
</p>
</details>

<details>
<summary> Part 7</summary>
<p>

```js
await contract.method7123949()
```
You'll get:
```
"If you know the password, submit it to authenticate()."
```
</p>
</details>

<details>
<summary> Part 8</summary>
<p>

```js
await contract
```
This pulls up ever thing about the contract. Look to the abi and you'll see that it has a password function
```js
await contract.password()
```
You'll get:
```
"ethernaut0"
```
</p>
</details>

<details>
<summary> Part 9</summary>
<p>

```js
await contract.authenticate("ethernaut0")
```
Then simply submit you answer with the orange button
</p>
</details>
