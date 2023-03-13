# networkstate
How to build a Service DAO/Network State on Solana


Token Issuance

There are multiple options for creating a new token. We have discovered that the initial distribution is when a community can expect to have its highest quorum. In our model, we have identified two main factors for deciding distribution of our Network State citizenships;  how active someone is as a voter and how often they receive a contribution payout from our treasury. These two allow us to maintain a high level of activity and resemble a meritocracy. Knowing how to target your conitrbutors is your top priority at genesis.

The token system that got us here is Strata Protocol. Strata enables token issuance associated with a bonding curve. Strata also has the additional beenfit of allowing the creation of taxes. These act as a tax on services within a network state; any participant can unwrap their membership tokens for instant liquidity or can hold on to them for more governance power. These taxes are necessary for growing the network state. 

Deans Token: 

var mint = new PublicKey("8upjSpvjcdpuzhfR1zriwg5NXkwDruejqNE9WNbPRtyA");
var curve = await tokenBondingSdk.initializeCurve({
    config: new TimeCurveConfig().addCurve(
      0, // 1 hour
      new ExponentialCurveConfig({
        c: 1/35,
        b: 0,
        pow: 2,
        frac: 1
      })
    )
});

var { ownerTokenRef, tokenBonding } = await tokenCollectiveSdk.createSocialToken({
  isPrimary: true,
  mint,
  collective: (await SplTokenCollective.collectiveKey(mint))[0],
  metadata: {
    name: "Dean's List",
    symbol: "DEAN",
    uri: "https://arweave.net/_ba7wTWOYnNCNSqLddKxc5It5jNGFNsgiUrkxvJfpBc",
  },
  tokenBondingParams: {
    curve,
    buyBaseRoyaltyPercentage: 5,
    buyTargetRoyaltyPercentage: 0,
    sellBaseRoyaltyPercentage: 30,
    sellTargetRoyaltyPercentage: 0
  }
});

Destination royalties were later updated to our Realms Governance - Aqz7UK6VCUaSosh72qQxV6vSpb7CKaegrkdu5eq3JRQM

You can swap for a DEAN token here https://app.strataprotocol.com/swap/6LyW1iUpfTPiMxSLMpKCxeAqXDz7nuWCfCNnEaSmibZ1

You can also purchase a token OTC from here https://coinablepay.com/@deans-list/ozWxnDy7G7B2Mxw2LLia72

Realms Creation

The first step in creating a DAO or Network State on Solana is the creation of a Realms instance. We chose to use the default instance which allows us to rely on the Realms community for updates and maintenance of our governance. 

Our process for raisining quorum over time and setting a proposal threshold are detailed in the article below. Our current model for activity has allowed us to achieve a consistent 50% quorum. A community should constantly strive to push it up, but do so with extreme caution.

https://medium.com/@deanmachine/voting-dynamics-setting-proposal-thresholds-and-quorum-for-your-tokenized-community-multisig-4cec9e0d5e05


Squads Creation

We use Squads to further distribute responsibility to our different department heads. Each Squad is responsible for its own budget that is voted on at the beginning of every month. Our current departments are:

Department of State - responsible for our external ecosystem
Department of Interior -  responsible for our internal ecosystem
Department of Labor - responsible for services
Department of Education - responsible for documentation
Department of Treasury - responsible for our treasury
Department of Development - responsible for development

Coinable Creation

Coinable is a no-code solution for selling services in web3. The store is here - https://coinablepay.com/store/deans-list
All sales go directly to our Realms Treasury address and new sales are posted directly into our Discord through webhook. 

Distributing compensation within services

Each service has a template for roles and responsibilities. We believe in a "no-claim" approach to work; no one person can become a bottleneck and all tasks are available to all citizens.

Here is an example template we use for our feedback service:
Our people are paid in USDC. Therefore their pay is not subject to volatility and speculative actions.

Usually the pool of money will be distributed as:

Feedback: 70% of the pool
Documentation: 8% of the pool
Management: 6% of the pool
Payout Calculation: 6% of the pool
Referral/Sales: 10% of the pool

Once the service is completed, this breakdown of compensation is presented and voted on in Realms. Eventually, as new services emerge, this voting system will possibly switch to a multi-sig for "heads of service". 
