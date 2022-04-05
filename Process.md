1) Application: present an application form based on a template that explore details of the assets on how it works, why meant to be added to Compound, list of questions:

    - Overview
        What is the token name and ticker symbol?
        What the the token do?
        What additional risks might supporting this token create?
        What audits, if any, have been done?
        Have there ever been any protocol hacks? If so, when? How were they addressed?
        Emergency contact for incidente response ?
    
    - Market Risk Information
        What venues allow for the trading of this asset?
        How much liquidity is there on each of these venues?
        How has that liquidity changed over time? One way to show this is with rolling 30/60/90 averages.
        What is the historical volatility of this asset?

    - Decentralization
        How is this asset distributed amongst token holders?
        GINI Coefficient
        Largest 10 positions and the percent of total float they constitute
        How is the supply of this currency controlled?
        Centralization scale (Centrally Backed → Permisionless)
    
    - Contracts related
        UAV
        More..

    - Parameters            
        Collateral Factor - will be 0 for all assets until after launch
        Reserve Factor (probably should start pretty high)
        Borrow Cap
        Interest Rate Curve
        Should likely start with an existing interest rate curve

    - Output should have a score

    - Monitoring reccomendations 

2) Automation & Implementation Review: 

    - Running tools: sanity checks, automatic detection on implementation/proxy
    - Testing: simulate governance proposal, accrue of interests, mint, redeem, borrow, repay, liquidations
    - Stress tests scenario (flash loans attacks, oracle manipulations etc) 
    - Deployment

3) Proposal: Pushing the Proposal and vote on it

4) Post-Launch Parameter Update: after launch, increasing collateral factor to a safe level and setting the reserve factor in line with other assets