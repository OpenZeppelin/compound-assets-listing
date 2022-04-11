1) Initialization: 
    - New market proposer reviews the [Checklist](Checklist.md) and provide as much as info they can (some fields are required) in a forum post titled "Add market: {ASSET SYMBOL}" under "New Market" category in [Compound forum]()

2) Community check:
    - Community handles back and forth to review that the info provided is correct and complete where required.

3) [WIP] Risk analysis: 
    - The community check output is a scoring mechanism that assign a score to the proposed market.
    - Gauntlet might conduct economic risk simulations to determine whether the token should be enabled as collateral, and if so, specify its risk parameterizations dependent on market conditions and ecosystem dynamics.

4) Tooling and simulations: 
    - Community run eth-saddle or any tool to check if the implemented contract matches the base implementation with the expected parameters.
    - Community execute available test suite and simulations.

5) Contracts deploy:
    - Promoter is asked to deploy the needed contracts (`CErc20Delegator`, `CErc20Delegate`, optionally a new `UniswapAnchoredView`) and provide their deployed address in the same forum post. Eventually contracts might need to be deployed on testnets if requested/needed.
    - At this point it should be clear wether the current oracle supports the new asset or if a new oracle must be deployed. If the latter is true, the proposal must come with a `setPriceOracle` call to change the oracle to the new version.
    - Promoter will provide verified contracts deployed and a diff will be evaluated to exclude eventual unwanted/unexpected codebase changes.

6) Proposal's draft: 
    - A formal proposal is drafted. It must include `supportMarket` and `setCollateralFactor` at least.

7) [WIP] Audit: 
    - Proposal is reviewed if the community asks for it.

8) Proposal submission: 
    - Proposal is submitted for voting.
    - If proposal fails, forum post is updated with results and follow up discussions can happen there.

9) Post-Launch Parameter Update: 
    - After launch, increasing collateral factor to a safe level and setting the reserve factor in line with other assets. 
    - Borrow limits can be optionally set.
