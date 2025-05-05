Zeru Credit Scoring – Methodology Overview
Scoring Wallet Behavior on Compound V2 Protocol
🎯 Goal
To design a decentralized, intelligent scoring system that assigns a credit score ranging from 0 to 100 for each wallet engaging with the Compound V2 protocol. The score is solely based on historical transaction patterns, with higher values reflecting responsible and consistent protocol use.

📦 Data Overview
Raw transaction-level data extracted from the Compound V2 ecosystem. These logs are segmented by interaction types such as:

deposit

borrow

repay

withdraw

liquidation

Each transaction entry includes:

account.id: Wallet identifier

amountUSD: Value of the transaction

timestamp: Recorded in UNIX format

✅ Traits of Wallet Behavior
🟢 Positive Indicators (High Score)
Consistent repayments over time

High collateral vs. borrowed amount

Continuous, long-term interaction

Very few or zero liquidation incidents

🔴 Negative Indicators (Low Score)
No repayment after borrowing

Isolated or abnormal usage activity

Frequent liquidations or protocol abuse

🔧 Feature Extraction & Behavioral Metrics
The following features are derived per wallet to model behavioral quality:

Feature	Description
total_txns	Total number of transactions
deposit_amt, borrow_amt, repay_amt, withdraw_amt	Aggregated monetary value for each type
repay_ratio	Ratio of repaid amount to borrowed amount
deposit_borrow_ratio	Comparison of deposits to borrowing volume
net_change	Collateral held = deposits - withdrawals
txn_frequency	Engagement rate = txns per active day
liquidations	Total number of liquidation incidents

🧮 Credit Scoring Logic
All derived features are normalized on a [0, 1] scale using min-max normalization. The final score is computed with this weighted formula:

makefile
Copy
Edit
Score = (
    0.40 * norm(repay_ratio) +
    0.20 * norm(deposit_borrow_ratio) +
    0.15 * norm(txn_frequency) +
    0.15 * norm(net_change) +
    0.10 * (1 - norm(liquidations))
) * 100
This approach gives priority to wallets that:

Fully or mostly repay their borrowed amounts

Maintain high collateralization

Interact regularly with the protocol

Steer clear of risky behaviors like liquidation

📤 Outputs
Python Script: solution.py contains the full pipeline

CSV File: top_1000_wallet_scores.csv lists the highest scoring wallets

Wallet Behavior Report: One-page summary that evaluates 5 top and 5 low-performing wallets

This scoring framework promotes transparent and meaningful credit behavior within the DeFi space, offering insights without relying on external datasets or prebuilt labels.

