👀 What is Re-Entrancy?

![image](https://github.com/ryuzaki364/Sample-ReentrancyAttack-SmartContracts-/assets/42649594/f9a3022b-2c60-4b00-8b82-4a89cfaf323f)

Re-Entrancy is the vulnerability in which if Contract A calls a function in Contract B, Contract B can then call back into Contract A while Contract A is still processing.

This can lead to some serious vulnerabilities in Smart contracts, often creating the possibility of draining funds from a contract.

Let's understand how this works with the example shown in the above diagram. Let's say Contract A has some function - call it f() that does 3 things:

1. Checks the balance of ETH deposited into Contract A by Contract B Sends the ETH back to Contract B
2. Updates the balance of Contract B to 0
3. Since the balance gets updated after the ETH has been sent, Contract B can do some tricky stuff here. If Contract B was to create a fallback() or receive() function in it's contract, which would execute when it received ETH, it could call f() in Contract A again.

Since Contract A hasn't yet updated the balance of Contract B to be 0 at that point, it would send ETH to Contract B again - and herein lies the exploit, and Contract B could keep doing this until Contract A was completely out of ETH.

