
# Protocol risks

## Security

- **Codebase bug**: smart contract bugs that might be exploited. For this reason Compound codebase went to [several round of audits](link)

- **External integrations failures**: Currently Compound depends on Uniswap v3 TWAP and Chainlink oracles integrations. Oracle manipulations can lead to price manipulations as described below. The `UniswapAnchoredView` contract enforce price swings to not be bigger than the `anchor` established mitigating partially the issue. The contract also stores a fallback mechanism to Uniswap v3 TWAP prices whenever price reporters become unreliable, and this might mitigate the issue assuming that:
    - Proper monitoring solutions are setup to detect any downtime on reporters as soon as possible.
    - Admin actions are taken to activate fallback mechanism on oracle and that the corresponding Uniswap v3 pool has enough liquidity to avoid pool liquidity manipulations.

## Governance

- **Wrong governance action**: A proposal containing dangerous transactions is executed. Like oversized COMP distribution issue. The B2DAO relation was born to remediate to this.

- **Governance attacks**: Concentration of big quantities of COMP (relative to thresholds and quorum paramters that might be present on Governance contract) through loans/buy in few wallets that might defeat governance itself. Potential but unrealistic, no examples have been found of such an attack.

## Market

- **Price manipulation**: If price manipulation happens in a low liquidity market, prices can changes fast and cause honest borrowers to be liquidated, being subjected to liquidation penalties.

- **Insolvency risk**: The value of the funds held by the protocol is less than the liabilities of the protocol.

- **Liquidity risk**: To be illiquid (not insolvent) depending on active borrows, borrow limits and collateralization ratios.

- **Not incentivized liquidations**: External prices for an asset can crash to the point that liquidators are not incentivized to execute liquidations, leaving the protocol unhealthy.

- **Cascade effect**: Liquidations affecting crash of market prices that causes more liquidations. Deflationary spiral.

Market risks are deeply analyzed in [Gauntlet's report](https://gauntlet.network/reports/compound)

# Asset specific risks:

## Compatibility

- **Extra asset features**

- **ERC20 deviations**

## Compliance

- **Asset decentralization level**

- **External codebase bug/hack**

# List of external tokens interactions:

## Protocols contracts that interact with ERC20 tokens and the relative functions interacting:

- In `CErc20`
    - `sweepToken`
    - `getCashPrior`
    - `doTransferIn`
    - `initialize`

- In `Comptroller`
    - `updateCompSupplyIndex`
    - `distributeSupplierComp`
    - `grantCompInternal`

- In `GovernorBravoDelegate` (only `COMP`)
    - `castVoteInternal`
    - `cancel`

## ERC20 functions involved:

- `balanceOf`
- `transferFrom`
- `totalSupply`
- `delegate` and `getPriorVotes` for `COMP` or `COMP` like tokens