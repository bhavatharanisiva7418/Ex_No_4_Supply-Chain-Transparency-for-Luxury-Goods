# Ex_No_4_Supply-Chain-Transparency-for-Luxury-Goods
# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.

# Algorithm:
The manufacturer records product creation details on-chain.

The product moves through different supply chain checkpoints.

The ownership of the product can be transferred securely.

Buyers can verify the product’s authenticity.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```

## Expected Output:
A luxury good (e.g., a Rolex watch) is registered on-chain.
<img width="1916" height="1022" alt="image" src="https://github.com/user-attachments/assets/f5238127-bd78-4b84-8cc4-a2a7526fc313" />


Ownership is transferred at every checkpoint.
<img width="1919" height="990" alt="image" src="https://github.com/user-attachments/assets/ae1ddb13-02c8-4b61-aae9-c4cca53ce8a6" />

Buyers can check the authenticity before purchasing.
<img width="1918" height="974" alt="image" src="https://github.com/user-attachments/assets/b3e9758c-e625-4e30-9072-a8f8ad7e7da8" />


## High-Level Overview:
Helps prevent counterfeit luxury goods.

Teaches real-world supply chain use cases.

## RESULT :
Thus the supply chain transperncy is supplied succesfully.
