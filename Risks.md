# Compound Asset Listing - Risks

## Protocol Risks

### Security Risks

- **Codebase bug**: smart contract bugs that might be exploited. For this reason Compound battle-tested codebase has gone through [several rounds of audits](https://docs.compound.finance/#security).

- **External integrations failures**: Currently Compound depends on Chainlink oracles for price data. Oracle manipulations can lead to price manipulations as described below in the market risk section.

### Governance Risks

- **Wrong governance actions**: A proposal containing dangerous transactions is executed. Like oversized COMP distribution issue. OpenZeppelin's relationship with Compound was set up out of the necessity to avoid having proposals undermining the protocol itself.

- **Governance attacks**: Concentration of big quantities of COMP (relative to thresholds and quorum parameters that might be present in the governance contracts) through loans/buy in few wallets that might defeat governance itself. This is a potential but unrealistic risk, as no concrete examples have been found.

### Market Risks

Market risks are deeply analyzed and covered in [Gauntlet's report](https://gauntlet.network/reports/compound). Notable considerations include:

- **Price manipulation**: If price manipulation happens in a low liquidity market, prices are more easily manipulated and can cause honest borrowers to be liquidated and subject them to liquidation penalties.

- **Insolvency risk**: The value of the funds held by the protocol is less than the liabilities of the protocol.

- **Not incentivized liquidations**: The prices can crash so much that liquidations are not profitable anymore, leading to a lack of incentivized liquidators.

- **Cascade effect**: Liquidations producing price crashes in external markets creating a deflationary spiral that triggers more liquidations. Some modifications have been proposed to mitigate this, specifically proposal [#49](https://compound.finance/governance/proposals/49).

We highly recommend going through the Gauntlet's report to understand how these risks are mitigated or addressed by the current protocol design.

### Network Risks

Compound smart contracts are deployed on many different networks each with their own dynamics, security models, and asset pools. Compound by venturing into these networks takes on risks surrounding network design, evm compatability, bridge security, native vs bridged asset dynamics and more.

## Asset-Specific Risks

All asset-specific risks should be addressed in a structured manner. OpenZeppelin proposes a [Checklist](Checklist.md) of topics to watch out for and evaluate when it comes to onboard new assets. Together with this checklist we provide a comprehensive [Process](Process.md) to follow for new assets listing.

### Compatibility

- **Extra asset features**: How extra features can have unwanted or unexpected effects on the ERC20 functions involved in Compound integration (listed at the end of this document).

- **ERC20 deviations**: Depending on how much the asset deviates from ERC20 standard, it might defeat basic protocol assumptions on how ERC20 tokens behave. Rebasing, deflationary or fees-driven tokens might give unexpected results on basic operations like `transfer` or `balanceOf`.

### Compliance

- **Asset decentralization level**: Having an asset highly centralized can lead to unexpected minting, and more if the asset has access control with centralized parties in power of it, where also transfer may unexpectedly fail for some blacklisting feature. It is important to asses sensitive asset's functionalities and determine the grade of decentralization.

- **External codebase bug/hack**: Assets are smart contracts as anything else and they might contain bugs that can be exploited at some point. Assessing how those bugs can cause issues with Compound means in the first instance to recognize them and later study their implications.

## List of external tokens interactions:

Lastly it is important to remark which are the concrete interactions between Compound and external asset's contracts.

### Protocols contracts that interact with ERC20 tokens (including cTokens) and the relative functions interacting:

- In `Comet`
	- `doTransferIn` relies on the ERC20 function `transferFrom`, and is called internally within Comet by many other functions:
		- `supply`, `supplyTo`, and `supplyFrom`. These are listed together since they all use the `supplyInternal` function.
		- `buyCollateral`, which calls `doTransferIn` for the "base" asset.
	- `doTransferOut` relies on the ERC20 function `transfer`, and is called internally by within Comet by many other functions:
		- `withdraw`, `withdrawTo`, and  `withdrawFrom`. These are listed together since they all use the `withdrawInternal` function.
		- `withdrawReserves`, an authorized function only callable by `governor` which only transfers out the "base" asset.
		- `buyCollateral`, which calls `doTransferOut` for the "collateral" asset.
	- `approveThis` relies on the ERC20 function `approve`. This function lets the `governor` give an approval of ANY token within the Comet system. 
	- `getPackedAssetInternal`, which is internal and only called within the constructor for `Comet`, calls the ERC20 function `decimals` as a sanity check against user input. Note that this will NOT be applied for new assets which are added to Comet outside of the initial construction.
	- `constructor` uses the ERC20 function `decimals` to check the decimals of the "base" token, but of course only during construction.
	- `getCollateralReserves` calls the ERC20 function `balanceOf` for some collateral asset.
	- `getReserves` calls the ERC20 function `balanceOf` for the "base" token.

- In `CometRewards`
	- `doTransferOut` calls the ERC20 function `transfer` for some token. It is called by `claimInternal` for transferring the configured reward token to the recipient, or it can be called via `withdrawToken` by the `governor` to transfer any token out of the contract.
	- `setRewardConfig` uses the ERC20 function `decimals` to setup rewards schemes. This function is only callable by the `governor`.
	
- In `BaseBulker`
	- `sweepToken` calls the ERC20 functions `balanceOf` and `transfer` (via `doTransferOut`) to allow only the `admin` to remove any asset from the bulker. 
	- `doTransferIn` calls the ERC20 function `transferFrom` to transfer ERC20 tokens to the bulker from a user. Note that any asset can be transferred. 
	
- In `MainnetBulker` (which inherits `BaseBulker`)
	- `withdrawStEthTo` uses `doTransferOut` to call the ERC20 function `transfer`. Note that this is specifically for withdrawing one type of token (`steth`)
	- `supplyStEthTo` uses `doTransferIn` to call the ERC20 function `transferFrom`, as well as function `approve` for both the `steth` and `wsteth` contracts, and function `wrap` in the `wsteth` contract. Note that these calls are for only the defined tokens, `steth` and `wsteth`.
	- MainnetBulker should be considered a special case, as this market is well-defined. It lends out ETH against different collaterals which are simply interest-bearing ETH. Still, it is technically possible for new assets to be listed in this market. Additionally, it is important to note that Lido Staked ETH (`steth` here) is a _rebasing_ token, which is why there are special functions defined for its transfer into and out of the protocol.

- In `GovernorBravoDelegate`
    - [`castVoteInternal`](https://etherscan.io/address/0x563a63d650a5d259abae9248dddc6867813d3f87#code#F1#L266) which is used internally to save the result of a vote cast. It uses the `getPriorVotes` function from COMP token.
    - [`cancel`](https://etherscan.io/address/0x563a63d650a5d259abae9248dddc6867813d3f87#code#F1#L156) which is used to cancel a proposal which is not being executed yet and that makes uses again of the `getPriorVotes` function from COMP token.

### [ERC20](https://eips.ethereum.org/EIPS/eip-20#methods) functions involved:

- `balanceOf`
- `transferFrom`
- `transfer`
- `decimals`
- `approve`
- `delegate` and `getPriorVotes` only for [`COMP`](https://etherscan.io/address/0xc00e94cb662c3520282e6f5717214004a7f26888#code) or `COMP`-like tokens
