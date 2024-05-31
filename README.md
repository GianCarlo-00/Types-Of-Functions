# Description

In Solidity, these kinds of functions are view, pure, and payable. Although they can read state variables and return their values, view functions cannot change any state variables. Pure functions are used to do out computations; they are not subject to mutation or reading of the contract variables.

### Executing Program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyTokenERC20 is ERC20 {
    address public owner;

    constructor(string memory _name, string memory _symbol,uint256 initialSupply) ERC20(_name, _symbol) {
     _mint (msg.sender, initialSupply);
     owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can call this function");
        _;
    }

    function mint(address _to, uint256 _amount) public onlyOwner {
        _mint(_to, _amount);
    }

    function burn(uint256 _amount) public {
        _burn(msg.sender, _amount);
    }

    function transfer(address _to, uint256 _amount) public override returns (bool) {
        require(_to != address(0), "ERC20: transfer to the zero address");
        return super.transfer(_to, _amount);
    }

    function transferFrom(address _from, address _to, uint256 _amount) public override returns (bool) {
        require(_to != address(0), "ERC20: transfer to the zero address");
        return super.transferFrom(_from, _to, _amount);
    }
}



# Author
MetaCrafter Gian

# License
This project is licensed under the MIT License - see the LICENSE.md file for details.
