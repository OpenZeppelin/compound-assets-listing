# Compound Asset Listing - Checklist

## Info that needs to be submitted by the proposer

*\* Indicates a required field*

### General

- [ ] Token Asset Name*
- [ ] A description of the project and the token*
- [ ] Benefits to Compound Community*
- [ ] Resources (Website, Social Media Links and docs)*
- [ ] The proposal author their contact info*
- [ ] The relationship between the author of the new market proposal and the token*
- [ ] Social channels Metrics (Size, activity and growth).

### Market Risk Assessment

- [ ] Market Cap of the token*
  - [ ] Minimum and maximum market cap of the token within the last 6 months.
  - [ ] Market Cap of token on Comet markets
- [ ] The largest exchanges where the token is listed and its respective liquidity*
- [ ] The largest smart contracts balances of tokens and what those contracts do.
- [ ] Provide the volatility of the token. Rolling windows of 1,3,6 & 12 month periods would be ideal. For more info see [Gauntlet's volatility guide](https://maker-report.gauntlet.network/int_vol).
- [ ] Total supply*
- [ ] Emission schedule.

Note: Gauntlet will also pull live data to conduct their [market risk assessment](https://gauntlet.notion.site/gauntlet/Gauntlet-Market-Risk-Framework-for-Asset-Listings-on-Compound-de5a852131514f14a560be56b6e51419) after the Checklist is submitted.

### Decentralization

- [ ] How is this asset distributed amongst token holders? List the top 10 holders, the percentage of each holder, and tag any of them if they are known.*
- [ ] List all of the privileged roles in the token contract. This can include whitelisted EOAs, Multi-sigs or DAOs.*
- [ ] Is it pausable?*
- [ ] Does it have a blacklist or whitelist?*

### Smart contract risks

#### Codebase & On-chain Activity:
- [ ] Provide a Github repository for the underlying token contracts*
- [ ] Provide a test suite with code coverage.
- [ ] Provide Etherscan links with verified contracts*
- [ ] Give the age of the token in days*
- [ ] Given the number of transactions in the contract to date*

#### Security Posture:
- [ ] What audits, if any, were performed? Provide links to the reports if they exist.*
- [ ] Does the project have an active bug bounty program?*
- [ ] Provide emergency contacts with their responsiveness levels and response availabilities* 
- [ ] List additional security and formal verification tools used in development
- [ ] List all monitoring services used by the token, if any.

#### Multi-Chain Strategy
- [ ] Will the token include implementations on other networks*?
  - [ ] If so, will the tokens be natively minted on the other networks or bridged across?
  - [ ] Are there any mitigations in the contracts in case a bridge becomes inoperable or compromised?

#### Token contract Behavior:
- [ ] Does the token have more than one address[^1]?*
- [ ] Does the token use a compiler version greater than 0.8.0 or the SafeMath? If not, explain how the protocol deals with possible overflows and underflows*
- [ ] During the execution of the token's functions, does the token execute external code chosen by the caller or receiver?[^2] If so, please explain the reasoning behind this decision*
- [ ] How does the token contract deviate from a standard implementation of ERC20? Any additional features that the Compound DAO should know about?*
- [ ] Is it burnable?*
- [ ] Does the token contract have a fallback function? If so, when does it revert?[^3]
- [ ] Does it have a fixed supply? If no, who can mint?*
- [ ] Is it a rebasing token?*
- [ ] Does the token charge fees on transfers?*
- [ ] Does it implements any transfer hooks? Or hooks on any method?*
- [ ] Is the contract performing arbitrary `delegatecall`s?* If the answer is yes, indicate who can make these calls and to what contracts.
- [ ] Is it flash mintable? If yes, please provide more information on this feature*
- [ ] Is it flash loanable? If yes, please indicate who offers the service.*
- [ ] What are the typical gas costs for calling each of the standard ERC20 functions?
- [ ] If the token is a vault share (example: ERC-4626 token), is the exchange rate of the vault manipulable with the donation of a constituent asset of the vault?*

#### Price Feed Behavior
- [ ] Is the price feed supported by ChainLink?
  - [ ] If not, what entity is responsible for posting price updates? List names and addresses which may update the price feed
- [ ] How often will price updates be posted?
- [ ] At what price difference threshold will price updates be posted?
- [ ] Can the `AggregatorV3Interface` functions for this price feed ever revert when called?
- [ ] Does the bytecode of the custom price feed match an audited version?

#### Upgradability:
- [ ] Is it upgradeable?* If so:
  - [ ] Who is authorized to make an upgrade?
  - [ ] Can an upgrade happen instantaneously or is there a time-lock delay?
  - [ ] Which components are upgradable?
  - [ ] How does the upgradeability design work? Who manages it and are how upgrades performed?
  - [ ] Does it emit an event when the implementation is updated?
 
## Initial Requirements

- [ ] Set collateral factor to 0.
- [ ] Set established supply cap if necessary. Supply cap and collateral factor determine total borrowing power, and maximum liquidateable amount for the token.
      
## Considerations

- [ ] Proposals must be first posted in the Compound forum *New Markets* category.
- [ ] The on-chain proposal must contain a link to the corresponding thread in the forum.
- [ ] One proposal per asset.
- [ ] All actions in the proposal must be related to the listing of the token.
- [ ] Do not deploy contracts without first submitting the proposal to the forum.
- [ ] Use markdown in the description of the proposal in the transaction, add links and start the title with # Add market: NAME.

## Community Check
The community should review the following items before approving a new asset.

- [ ] Veracity or the info provided.
- [ ] Correct configuration of any new contracts (oracle, custom price feeds, asset).
- [ ] Documentation quality.
- [ ] Favorable results in the execution of the token test suite or integration simulations.

[^1]: [Double entry point vulnerability TUSD](https://blog.openzeppelin.com/compound-tusd-integration-issue-retrospective/).
[^2]: [C.R.E.A.M. Finance Post Mortem: AMP Exploit](https://medium.com/cream-finance/c-r-e-a-m-finance-post-mortem-amp-exploit-6ceb20a630c5).
[^3]: [Phantom Functions and the Billion-Dollar No-op](https://media.dedaub.com/phantom-functions-and-the-billion-dollar-no-op-c56f062ae49f)

