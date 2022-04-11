
# Protocol risks

## Security

- **Codebase bug**: smart contract bugs that might be exploited. For this reason Compound codebase went to [several round of audits](https://compound.finance/docs/security)

- **External integrations failures**: Currently Compound depends on Uniswap v3 TWAP and Chainlink oracles integrations. Oracle manipulations can lead to price manipulations as described below. The `UniswapAnchoredView` contract enforce price swings to not be bigger than the `anchor` established mitigating partially the issue. The contract also stores a fallback mechanism to Uniswap v3 TWAP prices whenever price reporters become unreliable, and this might mitigate the issue assuming that:
    - Proper monitoring solutions are setup to detect any downtime on reporters as soon as possible.
    - Admin actions are taken to activate fallback mechanism on oracle and that the corresponding Uniswap v3 pool has enough liquidity to avoid pool liquidity manipulations.

## Governance

- **Wrong governance actions**: A proposal containing dangerous transactions is executed. Like oversized COMP distribution issue. OpenZeppelin newborn relationship with Compound was born out of the necessity to avoid having proposals undermining the protocol itself being voted and executed.

- **Governance attacks**: Concentration of big quantities of COMP (relative to thresholds and quorum paramters that might be present on Governance contract) through loans/buy in few wallets that might defeat governance itself. Potential but unrealistic, no examples have been found of such an attack.

## Market

Market risks are deeply analyzed and covered in [Gauntlet's report](https://gauntlet.network/reports/compound) and they can be resumed in:

- **Price manipulation**: If price manipulation happens in a low liquidity market, prices can changes fast and cause honest borrowers to be liquidated, being subjected to liquidation penalties.

- **Insolvency risk**: The value of the funds held by the protocol is less than the liabilities of the protocol.

- **Liquidity risk**: To be illiquid (not insolvent) depending on active borrows, borrow limits and collateralization ratios.

- **Not incentivized liquidations**: External prices for an asset can crash to the point that liquidators are not incentivized to execute liquidations, leaving the protocol unhealthy.

- **Cascade effect**: Liquidations affecting crash of market prices that causes more liquidations. Deflationary spiral. Some modifications have been proposed to mitigate this, specifically proposal [#49](https://compound.finance/governance/proposals/49).

We highgly reccommend going through the Gauntlet's report to understand how those are mitigated by the current protocol design.

# Asset specific risks:

All assets specific risks (compatibility and compliance one) should be addressed in a structured manner. OpenZeppelin will propose a [Checklist](Checklist.md) of topics to watch out for and evaluate when it comes to onboard new assets. Together with this checklist we will provide a comprehensive process to follow for new assets listing.

## Compatibility

- **Extra asset features**: How extra features can have unwanted or unexpected effects on the ERC20 functions involved in Compound integration (listed below).

- **ERC20 deviations**: Depending on how much the asset deviates from ERC20 standard, it might defeat basic protocol assumptions on how ERC20 tokens behave. Rebasing, deflationary or fees-driven tokens might give unexepcted results on basic operations like `transfer` or `balanceOf`.

## Compliance

- **Asset decentralization level**: Having an asset highly centralized can lead to unexpected minting, and more if the asset has access control with centralized parties in power of it, where also transfer may unexpectedly fail for some blacklisting feature. It is important to asses sensitive asset's functionalities and determine the grade of decentralization.

- **External codebase bug/hack**: Assets are smart contracts as anything else and they might contain bugs that can be exploited at some point. Assessing how those bugs can cause issues with Compound means in the first instance to recognize them and later study their implications.

# List of external tokens interactions:

Lastly it is important to remark which are the concrete interactions between Compound and external asset's contracts.

## Protocols contracts that interact with ERC20 tokens (including cTokens) and the relative functions interacting:

- In `CErc20`
    - [`sweepToken`](https://etherscan.io/address/0x3363bae2fc44da742df13cd3ee94b6bb868ea376#code#F1#L124) to recover tokens mistakenly sent to the contract. This function `transfer`s out of the contract the entire contract's balance of the requested asset. It is callable only by the administrator. One fixed issue, was about this function not being protected over assets with a double entry point. Read more about it [here](https://blog.openzeppelin.com/compound-tusd-integration-issue-retrospective/).
    - [`getCashPrior`](https://etherscan.io/address/0x3363bae2fc44da742df13cd3ee94b6bb868ea376#code#F1#L147) which is used internally to retrieve contract's underlying `balanceOf`. It is important to notice how this function result can be manipulated. Read more about it [here](https://blog.openzeppelin.com/compound-comprehensive-protocol-audit/#ceth-and-cerc20-underlying-balances-can-be-manipulated).
    - [`doTransferIn`](https://etherscan.io/address/0x3363bae2fc44da742df13cd3ee94b6bb868ea376#code#F1#L161) used internally to move underlying tokens into the protocol by the use of `balanceOf` and `transferFrom` ERC20 methods. This function can handle non standard ERC20 and also accounts for fees-deducting assets like USDT.
    - [`initialize`](https://etherscan.io/address/0x3363bae2fc44da742df13cd3ee94b6bb868ea376#code#F1#L26) which is a single-call function used to setup proxy's storage when a new implementation is set. It uses the `totalSupply` function.

- In `Comptroller`
    - [`updateCompSupplyIndex`](https://etherscan.io/address/0xbafe01ff935c7305907c33bf824352ee5979b526#code#F4#L1184) used internally to update to a new value the index of the `supplyState` of COMPs on a specific asset. Together with it also the block number is saved to support latest index's update. It checks the `totalSupply` of the cToken contract.
    - [`distributeSupplierComp`](https://etherscan.io/address/0xbafe01ff935c7305907c33bf824352ee5979b526#code#F4#L1226) used internally to update the `compAccrued` and `compSupplierIndex` mappings to latest value, actually accruing COMP on user positions. It uses the `balanceOf` function.
    - [`grantCompInternal`](https://etherscan.io/address/0xbafe01ff935c7305907c33bf824352ee5979b526#code#F4#L1371) which is used internally to send COMP tokens to the users. It uses the `transfer` function.

- In `GovernorBravoDelegate`
    - [`castVoteInternal`](https://etherscan.io/address/0x563a63d650a5d259abae9248dddc6867813d3f87#code#F1#L266) which is used internally to save the result of a vote cast. It uses the `getPriorVotes` function from COMP token.
    - [`cancel`](https://etherscan.io/address/0x563a63d650a5d259abae9248dddc6867813d3f87#code#F1#L156) which is used to cancel a proposal which is not being executed yet and that makes uses again of the `getPriorVotes` function from COMP token.

## [ERC20](https://eips.ethereum.org/EIPS/eip-20#methods) functions involved:

- `balanceOf`
- `transferFrom`
- `totalSupply`
- `delegate` and `getPriorVotes` only for [`COMP`](https://etherscan.io/address/0xc00e94cb662c3520282e6f5717214004a7f26888#code) or `COMP`-like tokens