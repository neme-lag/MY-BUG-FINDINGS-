# MY-BUG-FINDINGS-

lists of some of my findings both in comp audit , private and bug bounty, exempting duplicates, only paid ones


# Project Title : HAEDAL PROTOCOL on @immmunefi
severity: high(1) & low(1)...Dup

# Project Title : BUCKET PROTOCOL on @immunefi
Severity : high(1)...Dup

# Project Title : XORCA on @immunefi 
severity:high(1) & medium (1)...Dup

# Project Title : DECENTRALAND on @immunefi
severity: medium(1).. Dup

# Project Title: REVERT FINANCE on @cantina

Severity : MEDIUM

## Key Findings & Results
Title: Fee Calculation Asymmetry Between Exact Input and Exact Output

File:  src/Swap.sol 
Functions:  _swapExactInput() ,  _swapExactOutput() 

Description
The fee calculation is asymmetric between exact-input and exact-output swaps. For exact input, fees are computed on the output amount ( rawAmountOut ). For exact output, fees are computed on the input amount ( rawAmountIn ). In imbalanced pools, these amounts can differ significantly, leading to inconsistent effective fee rates.

## Data sources and size
Repository: revert-finance/stableswap-hooks
Branch: main
Commit: cf0c30e576f144809df9819f4d3ad49e0b7fe2d7
In scope: All Solidity (.sol) files under the src/ directory. Files outside src/ (including test/, script/, and lib/) are out of scope.
Total nSLOC: ~1,348 across 12 .sol files

Status: Fixed

## Approach & Methodology
Tool used : Manual review

## Tech Stack
- Languages: Solidity



# Project Title: MONETRIX on @codearena

## Key Findings & Results
Title:PM slot auto-registration can brick accounting before HyperCore activates the 0x811 supplied slot.

Description
MonetrixVault.supplyToBlp registers a supplied slot in the Accountant synchronously via notifyVaultSupply, but the underlying ACTION_BORROW_LEND op=0 (supply) action is queued for HyperCore's end-of-block settlement phase. For the intervening window, HyperCore's 0x811 supplied_balance precompile reverts with PrecompileError when queried for an (account, token) pair whose PM slot has not been activated on L1 yet. MonetrixPrecompileReader.suppliedBalance has no try/catch on this precompile, the strict require(ok && res.length >= 128, ...) propagates the revert up through _readL1Backing → totalBackingSigned / totalBacking / surplus / distributableSurplus / yieldShortfall / settleDailyPnL. The whole Accountant pipeline DoS's for at least one EVM block, potentially longer.


## Data sources and size

https://code4rena.com/audits/2026-04-monetrix/submissions/S-763

Status : Fixed

## Approach & Methodology
Tool used : Manual review & Ai

## Tech Stack
- Languages: Solidity
