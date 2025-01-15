# Swap

The UniswapV2SwapExamples contract demonstrates how to interact with the Uniswap V2 Router to perform token swaps. It includes single-hop and multi-hop swaps with both "exact input" and "exact output" methods.

swapSingleHopExactAmountIn
Swap exact amount of WETH for specified minimum amount of DAI.
Returns amount of DAI received.

swapMultiHopExactAmountIn
Swap exact amount of DAI for specified minimum amount of USDC. WETH is traded as an intermediary (DAI->WETH->USDC)
Returns amount of USDC (target token) received.

swapSingleHopExactAmountOut
Swap maximum amount of WETH for exact amount of DAI. 
Returns amound of DAI received.

swapMultiHopExactAmountOut
Swap maximum amount of DAI for exact amount of USDC. WETH is traded as an intermediary (DAI->WETH->USDC)
Returns amount of USDC received.

IUniswapV2Router Functions called: 
swapExactTokensForTokens
swapTokensForExactTokens