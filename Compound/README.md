
# Compound 
Compound is a DeFi lending protocol that allows users to earn interest on their cryptocurrencies by depositing them into one of several pools supported by the platform. It is a decentralized application (DApp) that works on top of the Ethereum network. The platform works by letting users contribute or deposit crypto funds into a liquidity pool in order to earn interest on their assets. Users can currently use 20 different cryptocurrencies and the top three markets in Compound are ETH, USDC and WBTC.

## Compound protocol 
Compound is a protocol on the Ethereum blockchain that establishes money markets based on the supply and demand for the asset. Suppliers (and borrowers) of an asset interact directly with the protocol, earning (and paying) a floating interest rate.

### Supplying Assets
Unlike an exchange or peer-to-peer platform, where a user’s assets are matched and lent to another user, the Compound protocol aggregates the supply of each user; when a user supplies an asset, it becomes a fungible resource. This approach offers significantly more liquidity than direct lending and users can withdraw their assets at any time.

Each time users lock in funds with Compound, the platform will temporarily convert their holdings to cTokens that represent the value of the crypto they put in and therefore their stake in the pool.

### Borrowing Assets
Compound allows users to frictionlessly borrow from the protocol, using cTokens as collateral, for use anywhere in the Ethereum ecosystem.
 Each market has a collateral factor, ranging from 0 to 1, that represents the portion of the underlying asset value that can be borrowed. The sum of the value of an accounts underlying token balances, multiplied by the collateral factors, equals a user’s borrowing capacity .

### Collateral Value
Assets held by the protocol (represented by ownership of a cToken) are used as collateral to borrow from the protocol. To take out a loan on Compound, you must “overcollateralize” your loan. This means you need to have more funds locked in with Compound than your loan is worth.

### Risk & Liquidation
If you decide not to repay your loan on Compound, the automated contract will simply subtract the value of the loan from the value you hold in Compound as collateral which can never be less than the loan.

### Interest Rate Model
Compound protocol interest rate equilibrium is based on supply and demand. Interest rates should increase as a function of demand; when demand is low, interest rates should be low, and vise versa when demand is high.
 The utilization ratio U for each market a unifies supply and demand into a single variable: U = Borrows / (Cash + Borrows)
The interest rate earned by suppliers is implicit , and is equal to the borrowing interest rate, multiplied by the utilization rate.

## Implementation & Architecture
At its core, a Compound money market is a ledger that allows Ethereum accounts to supply or borrow assets, while computing interest. The protocol’s smart contracts will be publicly accessible and completely free to use for machines, dApps and humans.

### cToken Contracts
Each money market is structured as a smart contract that implements the ERC-20 token specification. User’s balances are represented as cToken balances; users can mint cTokens by supplying assets to the market, or redeem cTokens for the underlying asset.
The price (exchange rate) between cTokens and the underlying asset increases over time, as interest is accrued by borrowers of the asset.

### Borrowing
A user who wishes to borrow and who has sufficient balances stored in Compound may call borrow(uint amount) on the relevant cToken contract. This function call checks the user’s account value, and given sufficient collateral, will update the user’s borrow balance, transfer the tokens to the user’s Ethereum address, and update the money market’s floating interest rate.

### Liquidation
If a user’s borrowing balance exceeds their total collateral value (borrowing capacity) due to the value of collateral falling, or borrowed assets increasing in value, the public function liquidate(address target, address collateralAsset, address borrowAsset, uint closeAmount) can be called, which exchanges the invoking user’s asset for the borrower’s collateral, at a slightly better than market price.

### Price Feeds
A Price Oracle maintains the current exchange rate of each supported asset; the Compound protocol delegates the ability to set the value of assets to a committee which pools prices from the top 10 exchanges. These exchange rates are used to determine borrowing capacity and collateral requirements, and for all functions which require calculating the value equivalent of an account.

### Comptroller
The Compound protocol does not support specific tokens by default; instead, markets must be whitelisted. This is accomplished with an admin function, supportMarket(address market, address interest rate model) that allows users to begin interacting with the asset. In order to borrow an asset, there must be a valid price from the Price Oracle; in order to use an asset as collateral, there must be a valid price and a collateralFactor.
Each function call is validated through a policy layer, referred to as the Comptroller ; this contract validates collateral and liquidity, before allowing a user action to proceed.

### Governance
Compound will begin with centralized control of the protocol (such as choosing the interest rate model per asset), and over time, will transition to complete community and stakeholder control.
The following rights in the protocol are controlled by the admin:
- The ability to list a new cToken market 
- The ability to update the interest rate model per market 
- The ability to update the oracle address 
- The ability to choose a new admin, such as a DAO controlled by the community; because this DAO can itself choose a new admin, the administration has the ability to evolve over time, based on the decisions of the stakeholders.
