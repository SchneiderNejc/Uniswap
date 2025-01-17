# Swap
The UniswapV2SwapExamples contract demonstrates how to interact with the Uniswap V2 Router to perform token swaps. It supports both single-hop and multi-hop swaps using "exact input" and "exact output" methods.

Functions:
swapSingleHopExactAmountIn

Swaps an exact amount of WETH for a specified minimum amount of DAI.
Returns: The amount of DAI received.
swapMultiHopExactAmountIn

Swaps an exact amount of DAI for a specified minimum amount of USDC.
WETH is used as an intermediary (DAI → WETH → USDC).
Returns: The amount of USDC (target token) received.
swapSingleHopExactAmountOut

Swaps up to a maximum amount of WETH for an exact amount of DAI.
Excess WETH is refunded.
Returns: The amount of DAI received.
swapMultiHopExactAmountOut

Swaps up to a maximum amount of DAI for an exact amount of USDC.
WETH is used as an intermediary (DAI → WETH → USDC). Excess DAI is refunded.
Returns: The amount of USDC received.
Uniswap V2 Router Functions Utilized:
swapExactTokensForTokens

Swaps an exact input token amount for as many output tokens as possible (based on slippage and liquidity).
swapTokensForExactTokens

Swaps as few input tokens as necessary to receive an exact output token amount.# Flash swaps
A flash swap is a feature of Uniswap V2 that allows you to borrow tokens from a liquidity pool without providing upfront collateral, provided you repay the borrowed amount plus a small fee within the same transaction. This atomicity ensures that either all steps of the operation are completed successfully, or the transaction is reverted.
This feature is useful for arbitrage, collateral swaps, or other advanced DeFi strategies.

How It Works:

A user initiates a swap function with parameters specifying the desired token and amount.
Uniswap provides the requested tokens but expects the repayment (plus a 0.3% fee) within the same transaction.
If the repayment conditions aren't met, the transaction reverts, ensuring liquidity providers face no risk.


Uniswap V2 Flash Swap
Flash swaps on Uniswap V2 enable users to borrow tokens from a liquidity pool without upfront collateral, as long as the borrowed amount is returned (plus a fee) by the end of the transaction. This functionality supports advanced use cases like arbitrage, refinancing, and liquidations within a single atomic transaction.

Key Concepts:
Why It's Needed:
Flash swaps are useful when users need temporary access to liquidity for advanced DeFi strategies without holding the upfront capital for the required tokens.

How It Works:

A user initiates a swap function with parameters specifying the desired token and amount.
Uniswap provides the requested tokens but expects the repayment (plus a 0.3% fee) within the same transaction.
If the repayment conditions aren't met, the transaction reverts, ensuring liquidity providers face no risk.
Benefits:

No Collateral: Borrow tokens without providing upfront capital.
Atomic Execution: Ensures all operations complete within a single transaction or revert entirely.
Flexibility: Supports complex DeFi use cases like arbitrage, liquidation, or refinancing.
Use Cases:

Arbitrage between different markets or exchanges.
Liquidating undercollateralized loans.
Refinancing debt positions.
Functions
flashSwap

Triggers the flash swap by specifying the amount of WETH to borrow.
Encodes data for the uniswapV2Call callback function.
uniswapV2Call

Automatically called by the Uniswap V2 pair contract after tokens are transferred.
Processes custom logic (e.g., arbitrage) and ensures repayment of the borrowed amount plus fees.
Implements a 0.3% fee calculation on the borrowed amount and transfers the fee from the user.
swap (in IUniswapV2Pair)

Facilitates the actual transfer of tokens to the borrower and invokes the uniswapV2Call callback.

Use Cases:
Arbitrage: Profit from price discrepancies across platforms or tokens.
Collateral Swapping: Replace collateral in lending protocols with a different token.
Flash Loans Replacement: Serve as an alternative to traditional flash loans for certain operations.
the 0.3% fee is the standard fee charged by Uniswap V2
