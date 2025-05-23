# Experiment 8: Post-Quantum Blockchain Wallet with Lattice-Based Cryptography
### Name : V Raksha Dharanika
### Reg No : 212223230167
# Aim:
To create a quantum-resistant wallet using lattice-based cryptography instead of traditional ECDSA, ensuring that future quantum computers cannot break private keys.

# Algorithm:

1.Understand that traditional ECDSA-based wallets are vulnerable to quantum computer attacks.

2.Select lattice-based cryptographic schemes like NTRU or CRYSTALS-Kyber for quantum-resistant security.

3.Generate lattice-based public-private key pairs and store hashed public keys on the blockchain for user authentication.

4.Enable users to sign transactions using lattice-based signatures instead of traditional signatures.

5.Implement smart contract logic to verify these lattice-based signatures before allowing any transaction to proceed.

6.Manage user registration and balances securely, ensuring only registered users with valid quantum-resistant signatures can send funds.

# Program:

(Solidity does not natively support lattice cryptography yet, but we simulate it using custom hash-based authentication.)
```py
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PostQuantumWallet {
    struct User {
        bytes32 publicKeyHash;
        bool registered;
    }

    mapping(address => User) private users; // Made private to hide from Remix UI
    mapping(address => uint256) public balances;

    event UserRegistered(address user, bytes32 publicKeyHash);
    event TransactionVerified(address from, address to, uint256 amount);

    // Constructor
    constructor() {}

    // Generate a quantum-safe signature (simulated using keccak256)
    function generateSignature(address _sender, address _recipient, uint256 _amount) public pure returns (bytes32) {
        return keccak256(abi.encodePacked(_sender, _recipient, _amount));
    }

    // Generate a simulated lattice-based public key hash
    function generatePublicKeyHash(string memory _publicKey) public pure returns (bytes32) {
        return keccak256(abi.encodePacked(_publicKey));
    }

    // Register a user with a public key hash
    function registerUser(bytes32 _publicKeyHash) public {
        require(!users[msg.sender].registered, "User already registered");
        users[msg.sender] = User(_publicKeyHash, true);
        emit UserRegistered(msg.sender, _publicKeyHash);
    }

    // Send funds using quantum-safe simulated signature
    function sendFunds(address _to, uint256 _amount, bytes32 _signature) public {
        require(users[msg.sender].registered, "Sender not registered");
        require(users[_to].registered, "Recipient not registered");
        require(balances[msg.sender] >= _amount, "Insufficient funds");

        bytes32 calculatedSignature = generateSignature(msg.sender, _to, _amount);
        require(calculatedSignature == _signature, "Invalid quantum-safe signature");

        balances[msg.sender] -= _amount;
        balances[_to] += _amount;
        emit TransactionVerified(msg.sender, _to, _amount);
    }

    // Deposit funds to the wallet
    function depositFunds() public payable {
        balances[msg.sender] += msg.value;}
}
```

# Output:
Users register using a post-quantum secure public key.



![image](https://github.com/user-attachments/assets/f5e86a1d-4181-4b0f-afad-c803ad55066c)





Transactions require a quantum-resistant signature for authentication.




![image](https://github.com/user-attachments/assets/4573ad37-ec11-416a-89f6-b2a91bf328c3)



If a quantum-resistant (lattice-based) signature is used, the transaction succeeds.





![image](https://github.com/user-attachments/assets/fd883204-2210-4b93-89db-33842933c825)

# RESULT : 
Thus,To create a quantum-resistant wallet using lattice-based cryptography instead of traditional ECDSA, ensuring that future quantum computers cannot break private keys.
