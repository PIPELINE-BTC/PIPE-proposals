
# Proposal: PRC-998 - Creating Composable Asset on Bitcoin

## Description

The PRC-998 proposal introduces a composable asset standard built on the Pipe protocol for Bitcoin, inspired by ERC-998 but optimized for Bitcoin's UTXO model. The goal is to provide a secure, efficient, and flexible mechanism for linking child assets to a parent asset without the vulnerabilities and high costs associated with Ethereum's smart contracts.

By leveraging Bitcoin's security and immutability, PRC-998 ensures that assets are preserved and scalable for various use cases, offering new possibilities for builders and developers on the Bitcoin network.

## Objectives

- **Enhance Composability**: Enable the creation of complex parent-child relationships for assets on Pipe.
- **Leverage Security**: Utilize Bitcoin's robust blockchain for long-term asset survivability.
- **Reduce Costs**: Avoid the need for smart contract interactions, minimizing fees.
- **Optimize UTXO Usage**: Ensure efficient and scalable data handling.

## Proposed Solution

### Parent-Child Linking via Public Key Authority

- **Authority Mechanism**: The public key used during the creation of the parent Pipe asset grants or denies rights to attach child assets.
- **Evolution Tree**: Using private keys of the collection, an evolution tree can be created with the collection's public key as the root.

### Example Structure

```text
Root Public Key
 |
 Pipe Asset 1 (Parent)
 |
 — — Public Key Authority (PKA)
 |                |
Pipe Asset 2    Pipe Asset 3
 |                |
Child Asset 4   Child Asset 5
```

### Comparison to Ordinals

PRC-998 eliminates the need to spend parent assets during child creation, avoiding destruction and inefficiencies associated with other methods like Ordinals. This approach supports dynamic, flexible hierarchies and preserves parent assets.

## Benefits

1. **Web3 Gaming**: Represent player characters as parent tokens with child tokens for achievements, items, and progression.
2. **Real-World Assets**: Simplify ownership transfer with parent tokens for properties and child tokens for related documentation.
3. **Digital Identity**: Link credentials to a parent identity token for verifiable blockchain-based resumes.
4. **Dynamic Websites**: Represent website components as child tokens linked to a parent, enabling version tracking and updates.
5. **Supply Chain Management**: Track components of a product as child tokens linked to a parent token for transparency and authenticity.
6. **Intellectual Property**: Manage licenses and derivative works with child tokens linked to a parent token representing the original asset.

## Addressing Scalability

- Optimized data handling minimizes on-chain storage.
- Future integration with the Lightning Network ensures low-cost, scalable transactions.

## Future Directions

PRC-998 is designed with scalability and versatility in mind, opening the door to a broad range of use cases while maintaining Bitcoin's core principles of security and decentralization.
