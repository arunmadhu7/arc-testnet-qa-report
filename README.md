# arc-testnet-qa-report
Manual QA testing report for ARC Testnet DeFi dApp (Flow)
ARC Testnet QA Artifact

Project: ARC Testnet
QA Engineer: Arun Madhusoodanan
Date: 30-Jan-2026
Environment: MetaMask, Windows / Chrome
dApp: Flow (flowonarc.xyz)

1. Environment Setup

• Added ARC testnet to MetaMask using official RPC parameters
• Verified successful network addition with no configuration or RPC errors
• Confirmed network visibility and chain selection within MetaMask

Scope excluded:
• Wallet–dApp connection
• Functional interaction testing

2. Testnet Funding (Pre-condition)

• Received ARC testnet tokens via official faucet
• Faucet interaction completed successfully
• Testnet token balance verified in MetaMask

Scope excluded:
• Transaction execution

3. Wallet ↔ dApp Connection

Scope:
• Wallet connection flow
• Network handling behavior

Observations:
• Wallet connection initiated from Flow dashboard using MetaMask
• Wallet connection approved successfully
• dApp automatically switched wallet network to ARC mainnet on initial connection
• Dashboard state updated correctly after successful connection

Edge case issue:
• Manually switched MetaMask network to Ethereum after connection
• Attempted to interact with dApp CTA while on non-ARC network
• CTA became unresponsive
• No network switch prompt, warning, or error message shown
• Recovery possible only after manually switching back to ARC network or fully disconnecting and reconnecting MetaMask

Expected behavior:
• Detect wallet network mismatch
• Prompt user to switch back to ARC network or display clear guidance

Actual behavior:
• Silent failure when wallet is on non-ARC network
• Manual recovery required

Severity:
• Medium — user interaction blocked without explanation

Evidence:
• flow-arc-network-mismatch-unresponsive-cta.mp4

3a. Wallet Disconnect / Dropdown Issue

Observation:
• Clicking the connected wallet address does not open any dropdown or menu
• No option exists to disconnect the wallet from inside the dApp
• Wallet can only be disconnected externally via MetaMask or page reload and reconnect

Impact:
• Medium to High UX issue
• Users cannot manage wallet sessions from within the dApp

Expected behavior:
• Clicking wallet address opens a dropdown menu with:
• Disconnect wallet
• Copy address
• View on explorer (optional)

Actual behavior:
• No dropdown
• No disconnect option

Severity:
• Medium — blocks wallet session management and may lead to accidental actions on the wrong network

Evidence:
• wallet-no-dropdown.mp4

Recommendation:
• Implement wallet dropdown with a clear “Disconnect” option
• Optionally include network status or quick network switch

4. Read-Only Dashboard (ARC Testnet)

Observations:
• dApp opened without wallet shows global stats correctly
• Wallet section displays “Connect wallet”
• Wallet connected shows address and balances correctly
• Wallet on wrong network displays warning and pauses read calls
• Page refresh or reconnect updates data correctly
• No stale values observed
• No console or RPC errors detected

Summary:
• Read-only dashboard functions correctly
• Wallet disconnect menu missing (see section 3a)

5. Transaction Testing (ARC Testnet)

Flows tested:
• Swap
• Lend
• Borrow
• Repay
• Withdraw

Observations:
• All transactions submitted successfully
• Transactions confirmed on-chain
• UI updated correctly after each transaction
• Balances and positions reflected accurately
• Wallet prompts appeared correctly
• No transaction or RPC errors observed

Summary:
• All core transaction flows working as expected

6. Failure and Edge Case Testing

Observations:
• Insufficient balance blocks transaction with clear error message
• Wrong network before action prevents transaction and displays warning
• Network changed during active transaction stops execution safely
• No on-chain execution when network changes mid-flow
• User rejected transaction resets UI correctly
• Rapid multiple clicks do not trigger duplicate transactions
• Wallet disconnected externally is detected and dApp resets to connect-wallet state

Summary:
• Failure scenarios handled safely
• No inconsistent UI or on-chain state observed

7. Overall Summary

• Environment and faucet setup verified successfully
• Wallet connection flow works but lacks network mismatch recovery UX
• Wallet disconnect functionality missing inside the dApp
• Read-only dashboard behaves correctly
• Core transaction flows fully functional
• Failure and edge cases handled safely

Next steps:
• Add network mismatch detection with user prompts
• Implement wallet dropdown with disconnect option
• Continue regression testing on upcoming builds

Artifact status:
• QA completed
