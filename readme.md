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