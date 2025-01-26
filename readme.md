Uniswap V2

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

Swaps as few input tokens as necessary to receive an exact output token amount.


# Uniswap V2 Add/Remove Liquidity

The UniswapV2AddLiquidity contract provides methods to interact with the Uniswap V2 Router for adding and removing liquidity in token pairs.

Functions:
addLiquidity

Adds liquidity to a Uniswap V2 pool for a specified token pair.
Steps:
Transfers _amountA and _amountB of _tokenA and _tokenB from the sender to the contract.
Approves the Uniswap V2 Router to spend the tokens.
Calls the router's addLiquidity function to deposit the tokens into the liquidity pool.
Returns:
amountA and amountB: Actual amounts of tokens deposited.
liquidity: Amount of liquidity tokens minted.
removeLiquidity

Removes liquidity from a Uniswap V2 pool for a specified token pair.
Steps:
Fetches the liquidity pair's address using the Uniswap V2 Factory.
Transfers the contract's liquidity tokens to the router.
Calls the router's removeLiquidity function to withdraw the tokens from the pool.
Returns:
amountA and amountB: Amounts of tokens withdrawn.

# Optimal One-Sided Supply
Optimal one-sided supply is a strategy used in decentralized finance (DeFi) for efficiently adding liquidity to a token pair pool (like Uniswap) when you hold only one of the tokens in the pair. Instead of requiring both tokens in equal proportions, this method determines how much of the held token should be swapped for the other token to minimize slippage and maximize liquidity provision efficiency.

Key Concepts:
Why It's Needed:
Liquidity pools require a balanced ratio of two tokens (e.g., Token A and Token B). If you only hold Token A, simply swapping an arbitrary amount into Token B can lead to poor execution due to price impact (slippage) or inefficient use of your assets. Optimal one-sided supply solves this.

How It Works:

It uses a mathematical formula to calculate the exact amount of the held token to swap for the paired token. This ensures the least price impact and creates the most balanced liquidity addition.
After the swap, both tokens are added to the pool in proportion to the pool's current reserves.
Benefits:

Efficiency: Maximizes the use of your tokens, ensuring you're not adding liquidity unevenly.
Minimized Slippage: Reduces the price impact caused by large swaps in the pool.
Convenience: Automates the process of swapping and adding liquidity, requiring only a single token from the user.
Use Cases:

Users or protocols that hold only one token but want to provide liquidity to a specific pool.
Strategies for liquidity mining where one-sided input is preferred.

Functions:
getSwapAmount
Calculates the optimal amount of a token to swap for the other token in the pair based on the reserves and the input amount.
Returns: Optimal swap amount.

zap
Automates the one-sided liquidity supply process:

Swaps the optimal amount of _tokenA for _tokenB.
Adds both tokens as liquidity to the pool.

_swap (Internal)
Executes a token swap via Uniswap V2 Router

_addLiquidity (Internal)
Adds liquidity to the Uniswap V2 pool using the tokens available in the contract.

How It Works:

A user initiates a swap function with parameters specifying the desired token and amount.
Uniswap provides the requested tokens but expects the repayment (plus a 0.3% fee) within the same transaction.
If the repayment conditions aren't met, the transaction reverts, ensuring liquidity providers face no risk.

Why It's Needed:
Flash swaps are useful when users need temporary access to liquidity for advanced DeFi strategies without holding the upfront capital for the required tokens.

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
