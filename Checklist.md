# Compound Asset Listing - Checklist

## Info that needs to be submitted by the proposer

### General

- [ ] Name.
- [ ] Description.

### Market Risk Assessment

- [ ] Market Cap of the token.
- [ ] On which exchanges is the token listed and what is its respective liquidity?
- [ ] Indicate volatility of the token using Gauntlet formula.

### Decentralization

- [ ] How is this asset distributed amongst token holders? List the top 5 holders of the token and tag them in case they are known.
- [ ] List all the the privilege roles in the token contract.
- [ ] Is pauseable?
- [ ] Has a blacklist?

### Smart contract risk

- [ ] Etherscan link.
- [ ] Public repo link.
- [ ] What audits, if any, have been done?
- [ ] Age of the token in days.
- [ ] Number of transactions in the contract.
- [ ] Provide emergency contacts.
- [ ] List of all monitoring services used by the token, if any.
- [ ] Does the token have more than one address?
- [ ] Provide test suite with code coverage.
- [ ] Does the token use a compiler version greater than 0.8.0 or the SafeMath?
- [ ] During the execution of the token's functions, does the token execute external code chosen by the caller or receiver?
- [ ] Provide documentation.
- [ ] Formal verification
- [ ] How much does the token contract deviate from a standard implementation of ERC20? Any additional features Compound should know about?
- [ ] Is it upgradeable?
  - [ ] Who is authorized to make an upgrade?
  - [ ] Can an upgrade happen instantaneously or is there a time-lock delay?
  - [ ] Which components can be upgraded?


## Community Check

- [ ] Veracity or the info provided.
- [ ] Correct configuration of the contracts (cToken, oracle, etc.).
- [ ] Execute available test suite and simulations.
- [ ] Check documentation quality.

## Initial Requirements

- [ ] Collateral factor to 0
