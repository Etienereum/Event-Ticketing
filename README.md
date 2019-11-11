# Event Ticket

This directory is a [truffle project](https://truffleframework.com/docs/truffle/overview) that contains the required contract, migration and test files. In this exercise you are going to implement the EventTickets.sol and EventTicketsV2.sol contracts.

The contract files contain the Truffle framework and needed comments which shows the implementation of the contracts. There a set of tests (in javascript) to determine if the implementation of the contracts is correctly. As an additional challenge, [I tried writing some Solidity tests](https://truffleframework.com/docs/truffle/testing/writing-tests-in-solidity) in TestEventTicket.sol.


This project is configured to connect to a development blockchain running on localhost (port 8545). This is the default configuration for [Ganache CLI.](https://github.com/trufflesuite/ganache-cli)

You can test these contracts by running the development blockchain and then `truffle test` in the terminal.

## Event Ticket Requirements:

- The owner creates the event by setting the # of tickets, description and URL.
- The event can be viewed to confirm the details set.
- Tickets can be purchased by indicate the quantity of tickets with the amount of ether they pay the contract.
- Include the ability to refund the buyer.
- Include the ability for the owner to end the sale and withdraw the entire balance.


## High Level Steps:
- Created a struct with the following: description, website, tickets, sales, buyers as mapping, isOpen as boolean.
- Created a constructor and a modifier
- Created the functions: readEvent(), buyTickets(), getRefund(), endSale().

## Steps followed:

- Created the contract structure
- Create the needed state variables
- Used a constructor to define the description, the URL, the ticketsAvailable and set isOpen to true.
- Created a readEvent function that returns the description, the URL, tickets, sales and isOpen.
- Created a buyTicket function that checks that isOpen is true, the amount sent is greater or equal to the number of tickets x price of the tickets and that the tickets are in stock. 
  - allocated the number of tickets to the buyer
  - added the number of tickets to the total sales
  - calculated if any payment change is required and if so, send the change back to the sender
- Created a getRefund function by:
  - checked the purchaser is valid
  - got the number of tickets purchased
  - subtracted this from the total stock
  - removed the buyer from the event mapping
  - transfered the funds back to the sender/purchaser
- Created an endSale function that when called, will transfer the remaining contract balance to the owner and also set isOpen to false.