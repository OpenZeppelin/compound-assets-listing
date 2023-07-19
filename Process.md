# Process for New Asset Listing on Compoundv3

## 1. Request Asset Listing

- New market proposer reviews the [Checklist](Checklist.md) and provides as much of the requested information that they can (note the required fields) in a forum post titled "Add market: {ASSET SYMBOL}" under the "New Markets" category in the [Compound forum](https://www.comp.xyz/c/markets/9)

## 2. Community Analysis

- ### Verification
    - Community member(s) handles back and forth to review that the info provided is correct and complete.

- ### Risk Analysis
  - The community checks the market risks of the asset based on available data, potentially using a scoring system that would need to be created.
  - Gauntlet provides a [market risk assessment framework](https://gauntlet.notion.site/gauntlet/Gauntlet-Market-Risk-Framework-for-Asset-Listings-on-Compound-de5a852131514f14a560be56b6e51419) to be used at this stage.

- ### Tooling and Simulations 
  - Community member(s) run eth-saddle or any tool to check if the implemented contract matches the base implementation with the expected parameters.
  - Community member(s) execute available test suite and simulations. These must be performed against the contracts deployed on the target network.

## 3. Finalize Deployment

- ### Deploy Any Auxilary Contracts
  - Promoter is asked to deploy any price feed modifier (for example, `ScalingPriceFeed.sol`)  and provide any deployed contract addresses in the same forum post. In the future, contracts might need to be deployed on testnets as well. Price feed modifiers must implement the [`AggregatorV3Interface`](https://github.com/smartcontractkit/chainlink/blob/develop/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol) from ChainLink.
  - Promoter will provide verified contracts deployed and a diff will be evaluated to exclude eventual unwanted/unexpected codebase changes.

- ### Draft On-Chain Proposal
  - A formal proposal is drafted. It must include a call to `Configurator.addAsset()`, and all necessary parameters for the `AssetConfig` element required as input. It must explain the reasoning behind each proposed parameter value (e.g. `borrowCollateralFactor`, `liquidateCollateralFactor`, `liquidationFactor`, `supplyCap`, etc.)
  - `asset` MUST be the underlying asset to be added, `priceFeed` MUST be the address of either a ChainLink oracle or the optional price feed modifier, and `decimals` MUST be the number of decimals of the underlying token.

## 4. Proposal Audit (optional)
    
- Proposal is reviewed by security auditors if the community asks for it. _This can be done by OpenZeppelin or another third-party hired by the proposal author._

## 5. On-Chain Proposal Submission

- Proposal is submitted for voting.

- If proposal fails, forum post is updated with results and follow up discussions can happen there.

## 6. Post-Launch Setting of Parameters

- After launch, increasing collateral factor to a safe level and setting the reserve factor to be in line with other assets. 

- Borrow limits can be optionally set.
