- A user who supplies tokens is unable to withdraw them
    - Insolvency risk - the value of the funds held by the protocol is less than the liabilities of the protocol.
    - Liquidity risk - the funds users wish to withdraw are not available for withdrawal, though the protocol holds other tokens of sufficient value to eventually allow the withdrawal

- A user who borrows funds pays unnecessary fees
    - Someone manipulates the price of assets, either in the oracle or by taking advantage of limited market liquidity to create large price swings. This can cause liquidations on assets that belies expectation and borrowers would pay liquidation penalties
    - An interest rate curve for an asset creates swing in interest rates that would appear usurious

- A protocol hack or bug
    - Someone finds a vulnerability in the protocol that allows them to withdraw a ton of value from the protocol, often referred to as a protocol “hack”
    - An error in the honest execution of an action, in this case, adding a new asset, that could destroy or lose user funds
        - Assets that rebase like AMPL, which behave differently than standard ERC20s, can be prone to these issues. I’m not picking on AMPL here - it’s been added to AAVE after extensive testing and so it is a great example that when these risks arise, how they can be addressed.
