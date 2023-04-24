# Escrow-Smart-Contract
An escrow smart contract is a smart contract that can be used to facilitate secure transactions between two parties. This is an excellent way to learn how to create a smart contract that interacts with multiple parties and involves conditional transactions. The following code shows how to create a basic escrow smart contract:


pragma solidity ^0.8.0;


    contract Escrow {
        address public payer;
        address payable public payee;
        address public lawyer;
        uint256 public amount;

constructor(address _payer, address payable _payee, uint256 _amount) {
    payer = _payer;
    payee = _payee;
    lawyer = msg.sender;
    amount = _amount;
}

function deposit() payable public {
    require(msg.sender == payer, "Only payer can deposit funds.");
    require(msg.value == amount, "Deposit amount must match contract amount.");
}

function release() public {
    require(msg.sender == lawyer, "Only lawyer can release funds.");
    require(address(this).balance == amount, "Contract balance must match contract amount.");
    payee.transfer(amount);
}

function balanceOf() public view returns (uint256) {
    return address(this).balance;
}

