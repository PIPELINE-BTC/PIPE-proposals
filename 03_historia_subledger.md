
# Proposal: Historia - A Sub-Ledger for Pipe Historical Actions

## Description

The Historia proposal introduces a sub-ledger system specifically designed for the Pipe protocol. Its primary purpose is to store the historical record of actions processed in each PipeBlock (group of Pipe actions extracted from a Bitcoin block), enabling efficient management of blockchain reorganizations. This system builds upon the concepts introduced in the Atomic Processing of PipeBlock proposal, ensuring that all actions are logged atomically and consistently in a historical ledger.

By leveraging this historical ledger, the protocol can efficiently reverse actions during reorganization events, ensuring accurate state management and improved performance on blockchains prone to frequent reorganizations (e.g., Doge and Testnet).

## Objectives

- **Enhance Reorganization Handling**:
  - Efficiently manage blockchain reorganizations by maintaining a record of all processed actions in the sub-ledger.
  - Enable reversal of actions when reorganizations occur.

- **Improve Robustness**:
  - Provide a consistent and auditable record of actions for debugging, analysis, and recovery.

- **Configurability**:
  - Allow configurable parameters for the size and retention policy of the Historia ledger.
  - Enable automatic or manual invocation of reorganization handling.

## Proposed Solution

### Historia Sub-Ledger:
- A dedicated, configurable sub-ledger that stores all actions performed in each PipeBlock at the time of processing.
- Each entry in the Historia ledger will include:
  - Block reference
  - Action type (e.g., mint, transfer, deployment)
  - Action details (e.g., balances modified, tokens deployed)
  - Associated UTXOs

### Action Reversal:
- During a blockchain reorganization, the Historia ledger will be used to reverse actions, starting from the most recent block and progressing backward to older blocks.
- Examples of reversal actions:
  - **Mint**: Subtract the minted balance from the corresponding address.
  - **Transfer**: Reverse the transfer by returning balances to their previous state.
  - **Deployment**: Remove deployed tokens.

### Configurability:
- Define the number of blocks to retain in the Historia ledger for rollback purposes.
- Allow on-demand reorganization handling via a command or automated triggers when reorganizations are detected.

### Integration with Atomic Processing:
- Historia will work seamlessly with the atomic processing system, ensuring all actions are logged consistently and completely at the end of block processing.

## Benefits

- **Improved Reorganization Efficiency**:
  - Reverse actions systematically and accurately, ensuring consistent state even during frequent reorganizations.
- **Enhanced Debugging and Analysis**:
  - Provide a detailed, auditable history of all actions for tracing and verifying system behavior.
- **Optimized Storage**:
  - Configurable retention policies allow efficient use of resources by limiting the size of the Historia ledger.

## Example Workflow

1. **Normal Block Processing**:
   - Actions (e.g., mint, transfer, deployment) are processed atomically at the end of a block.
   - These actions are logged in the Historia ledger as part of the block finalization.

2. **Reorganization Handling**:
   - A reorganization event is detected.
   - The protocol uses the Historia ledger to reverse actions in the most recent blocks, starting with the current block and moving backward.
   - Once actions are reversed, the system processes the new chain and updates the Historia ledger accordingly.

## Implementation Plan

1. **Design and Develop Historia**:
   - Create the sub-ledger structure and integrate it with the existing atomic processing framework.
   - Ensure each processed block appends its actions to Historia.

2. **Add Reversal Logic**:
   - Implement reversal actions for minting, transfers, deployments, and other Pipe-related events.
   - Test reversal scenarios to ensure accuracy and consistency.

3. **Configurability and Commands**:
   - Add configuration options for the size and retention of the Historia ledger.
   - Provide commands or automated triggers for handling reorganizations.

4. **Testing and Deployment**:
   - Simulate reorganization scenarios to validate the effectiveness of Historia.
   - Deploy the system incrementally and monitor performance and reliability.

The Historia sub-ledger will be a crucial component for ensuring the robustness and scalability of the Pipe protocol, particularly in environments where reorganizations are frequent. Its ability to efficiently log and reverse actions will significantly enchance the protocol's reliability and usability.