# Simple Escrow Smart Contract
A secure Solana program that allows a buyer to deposit funds into an escrow account, 
which are only released to the seller once specific conditions are met."

## 📌 Project Overview
This project implements a **Simple Escrow** mechanism on Ethereum.  
It allows a **buyer** to lock funds into the contract, a **seller** to claim those funds once a condition is met, and the **buyer** to cancel the escrow before the seller claims.

## 🌍 Real-World Problem
In many online or remote transactions:
- Trust issues: The buyer fears sending money before receiving goods/services.
- Risk of fraud: The seller fears delivering goods/services but not getting paid.
- No neutral middleman: Traditional escrow services exist but are costly, slow, or centralized.
- Cross-border challenges: Payments across countries can be delayed, expensive, or blocked.
Example:
A freelancer delivers work to a client overseas. The client doesn’t want to pay upfront, and the freelancer doesn’t want to deliver without assurance of payment. Both sides risk losing money or time.


💡 Solution with Simple Escrow
Your smart contract directly addresses these pain points:
- Buyer locks funds: Guarantees the seller that money is available.
- Seller claims after condition is met: Ensures seller gets paid only when buyer approves or a condition (like deadline or oracle signal) is satisfied.
- Buyer can cancel before claim: Protects buyer if seller doesn’t deliver or conditions aren’t met.
- Trustless & transparent: No need for a bank or third-party escrow agent. The blockchain enforces rules automatically.
- Global & low-cost: Works across borders with minimal fees compared to traditional escrow services.

## 🎯 Impact
- For freelancers & clients: Secure payments without intermediaries.
- For e-commerce: Buyers can safely purchase from unknown sellers.
- For peer-to-peer deals: People can trade assets (like NFTs or tokens) with reduced fraud risk.


## 🔍 What the Contract Does
- **Buyer locks funds**: The buyer deposits ETH into the contract at creation.  
- **Seller claims funds**: The seller can withdraw funds once the buyer approves or a condition is satisfied.  
- **Buyer cancels before claim**: If the seller has not yet claimed, the buyer can cancel and retrieve their funds.  

This ensures trust between parties without requiring a centralized intermediary.

---

## 🎯 Why This Design Was Chosen
- **Simplicity**: Minimal logic for clarity and contest demonstration.  
- **Transparency**: All state changes are visible on-chain.  
- **Flexibility**: Can be extended to support ERC20 tokens, deadlines, or arbitration.  
- **Trustless**: Neither party can unfairly control funds once conditions are set.

---

## 🔄 State Changes (State Machine / Sequence)
The contract follows a simple sequence:

1. **Initialized** → Buyer deposits funds (`fundsLocked = true`).  
2. **Released** → Buyer approves release, seller claims funds (`fundsLocked = false`).  
3. **Canceled** → Buyer cancels before seller claims (`fundsLocked = false`).  

State transitions:
- `Initialized → Released` (buyer approves → seller withdraws).  
- `Initialized → Canceled` (buyer cancels).  
- Once `Released` or `Canceled`, the contract is finalized.

---

## 🔒 Security Checks Implemented
- **Access control**:  
  - Only buyer can deposit and cancel.  
  - Only seller can claim funds.  

- **Re-entrancy protection**:  
  - Funds are transferred after state update (checks-effects-interactions pattern).  

- **Validation**:  
  - Prevents double spending (funds can only be released or canceled once).  
  - Ensures only valid state transitions occur.  

---

## 🌐 Deployment Information

- **Network:** Solana Devnet
- **Program ID:** `4118MKuzhYvbNYmQjA9rkqveT5V2ksyo1tNRH3zrqXpo`
- **Explorer Link:** [View on Solana Explorer](https://explorer.solana.com/address/4118MKuzhYvbNYmQjA9rkqveT5V2ksyo1tNRH3zrqXpo?cluster=devnet)

---

## 📂 Repository Structure

* **`src/`**: Contains the Solana program source code.
    * **`lib.rs`**: The main entry point for the smart contract logic (Simple Escrow).
* **`tests/`**: Contains the test suite for the program.
    * **`anchor.test.ts`**: TypeScript tests to verify the escrow functionality.
* **`client/`**: Client-side scripts for interacting with the deployed program.


