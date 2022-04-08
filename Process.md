1) Initialization: new market proposer review the [checklist]() and provide as much as info they can (some fields are required) in a forum post titled "Add market: XXX" under "New Market" category in Compound forum

2) Community check: community handles back and forth to review that info provided is correct and complete.

3) Scoring: the community check output is a scoring mechanism that assign a score to the proposed market.

4) Promoter is asked to deploy the needed contracts (CErc20Delegator, CErc20Delegate, optionally a new UAV) and provide their deployed address in the same forum post.

5) Tooling and simulations: community performs run on unit tests and scenario simulations with the new asset

6) Proposal's draft: A formal proposal is drafted. It must include `supportMarket` and `setCollateralFactor` at least.

7) [OPTIONAL] OpenZeppelin audit: proposal is reviewed

8) Proposal submission: proposal is submitted.

9) If proposal fails, forum post is updated with results.

10) Post-Launch Parameter Update: after launch, increasing collateral factor to a safe level and setting the reserve factor in line with other assets. Borrow limits can be optionally set and a new oracle might be needed for the asset to work.
