# KToken Smart Contract

## Overview

KToken is an ERC20-compliant token with added functionalities such as minting, burning, and ownership transfer. The contract is built using the OpenZeppelin library for secure and standard implementation of ERC20 tokens and ownership management.

## Features

- **Minting:** Only the owner can mint new tokens.
- **Burning:** Any token holder can burn their tokens.
- **Ownership Management:** The contract allows the owner to transfer ownership or renounce it.
- **ERC20 Standard:** Implements the standard ERC20 functions including `transfer` and `transferFrom`.

## Prerequisites

- **Solidity Compiler:** Version 0.8.0 or higher.
- **Node.js and npm:** For running the deployment scripts.
- **Hardhat:** Ethereum development environment.

## Installation

1. **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/KToken.git
    cd KToken
    ```

2. **Install dependencies:**
    ```bash
    npm install
    ```

## Deployment

1. **Compile the contract:**
    ```bash
    npx hardhat compile
    ```

2. **Deploy the contract:**
    Modify the `scripts/deploy.js` script to include your deployment parameters:
    ```javascript
    async function main() {
        const [deployer] = await ethers.getSigners();
        console.log("Deploying contracts with the account:", deployer.address);

        const KToken = await ethers.getContractFactory("KToken");
        const kToken = await KToken.deploy("KToken", "KTK", 1000);

        console.log("KToken deployed to:", kToken.address);
    }

    main()
        .then(() => process.exit(0))
        .catch((error) => {
            console.error(error);
            process.exit(1);
        });
    ```

    Then run the deployment script:
    ```bash
    npx hardhat run scripts/deploy.js --network <network-name>
    ```

## Usage

Minting Tokens

Only the contract owner can mint new tokens.

```javascript
await kToken.connect(owner).mint(accountAddress, amount);

###Burning Tokens

Any token holder can burn their tokens.
await kToken.connect(holder).burn(amount);

### Transferring Tokens

Standard ERC20 transfer function.
await kToken.connect(sender).transfer(recipientAddress, amount);

### Transfer From

- Allows a spender to transfer tokens on behalf of the owner.

Approve an allowance:
await kToken.connect(owner).approve(spenderAddress, amount);

Transfer tokens using transferFrom:
await kToken.connect(spender).transferFrom(ownerAddress, recipientAddress, amount);

### Ownership Management

- Renounce Ownership
The current owner can renounce ownership, making the contract ownerless.
await kToken.connect(currentOwner).renounceOwnership();

- Transfer Ownership
The current owner can transfer ownership to a new owner.
await kToken.connect(currentOwner).transferOwnership(newOwnerAddress);

### Acknowledgments

OpenZeppelin for their secure and community-vetted contracts.
Hardhat for their development environment and tools.

### Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
Please make sure to update tests as appropriate.

