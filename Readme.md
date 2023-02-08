# Aptos

clone to the Aptos-core Repository.

```powershell
git clone https://github.com/aptos-labs/aptos-core.git
```

download Aptos cli

create a new folder

create starter files by using

```powershell
../aptos move init --name <folder name>
```

add the address in move.toml file

```toml
[addreses]
sender = "0xa1e3aa355555eb0b94cb3de6c98c1a5dd33c45a3647b3b5697c21d4719339b2e"
```

compile the file

```powershell
../aptos move compile --named-addresses sender=7e8697fe143bc36df4d3c90735af289939555319f06672b66402f37cc802c24d
```

create a new file in the Sources folder and write a smart Contract in .move file

create a tests folder and write down test code

```powershell
tests/{$MODULE_NAME}_tests.move
```

test the code by using following command

```powershell
../aptos move test --named-addresses sender=7e8697fe143bc36df4d3c90735af289939555319f06672b66402f37cc802c24d
```

- Points to be considered while working on aptos
    1. Security: Aptos is designed to be a secure platform, with strong encryption and consensus algorithms to protect against hacking, fraud and other forms of abuse. When working with Aptos blockchain, it is important to follow best practices for secure coding and to be aware of potential security threats.
    2. Consensus Mechanism: Aptos uses a consensus mechanism to ensure the integrity of the blockchain and to prevent malicious actors from tampering with the data. It is important to understand the consensus mechanism used by Aptos and to follow best practices for integrating with the blockchain.
    3. Network Effect: Aptos is designed to be a decentralized platform, where all participants have an equal voice and equal control over the data. It is important to understand the network effect of Aptos and to be aware of the potential consequences of large-scale adoption.
    4. Performance: Aptos is designed to be a fast and efficient platform, with low latency and high throughput. When working with Aptos blockchain, it is important to consider the performance implications of different use cases and to optimize the code for speed and efficiency.
    5. Interoperability: Aptos is designed to be an interoperable platform, with support for multiple programming languages and integration with other blockchain platforms. When working with Aptos blockchain, it is important to consider the interoperability implications of different use cases and to be aware of the potential benefits and drawbacks of integration.
    
- Points to be considered while using move
    1. Ownership Transfer: The main purpose of the **`move`** operation is to transfer ownership of an object from one variable to another. After a **`move`** operation, the original object is left in a valid but unspecified state, and should not be used.
    2. Performance: Moving objects can be more efficient than copying them, because it avoids the cost of copying the data. However, the performance advantage of moving over copying depends on the type of object and the specific use case.
    3. Object Validity: After a **`move`** operation, the original object is no longer considered to be valid. This means that any attempts to access or modify the object will result in undefined behavior.
    4. Rvalue References: In C++, **`move`** operations are typically performed using rvalue references, which are special references that can only bind to temporaries or rvalues. To enable **`move`** operations, objects should define a move constructor and a move assignment operator.
    5. Exception Safety: When using **`move`**, it is important to consider the exception safety of the code. If an exception is thrown during a move operation, the original object may be left in an undefined state, and the code may be unable to clean up any resources it was using.
