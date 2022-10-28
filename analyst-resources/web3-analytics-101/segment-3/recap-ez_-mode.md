# Recap, ez\_ mode

These notes pick up after the SQL recap in the video. To this point, we are able to compute metrics using Flipside's `ez_` tables and SQL aggregations, powered by `GROUP BY`, `CTE`s, and `JOIN`s.

In the session, we take a look at a past Uniswap bounty, reproduced below, to review these concepts.&#x20;

<details>

<summary>Uniswap Bounty 1</summary>

Show the number of active users (wallets) on Uniswap and Sushiswap over the past year.

Describe how they compare using at least two metrics (such as unique users per month, transactions per user per month, or anyhting you find interesting).

Give insights on the differences or changes between the two platforms.

Choose either Polygon, Ethereum, or both for your analysis.

</details>

There are a number of metrics one count compute and ways to compare these user metrics. From a high level, we can start answering this question by looking at the initiator of the transaction. By looking at [the docs](https://docs.flipsidecrypto.com/our-data/tables/ethereum\_core-tables), we confirm that `origin_from_address` is the address that created the transaction.

```sql
SELECT
    date_trunc('w', block_timestamp) AS _date,
    platform,
    COUNT(tx_hash) AS transaction_count,
    COUNT(DISTINCT origin_from_address) AS unique_swappers,
    transaction_count / unique_swappers AS tx_per_wallet 
FROM ethereum.core.ez_dex_swaps
WHERE block_timestamp::DATE >= CURRENT_DATE - 365
    GROUP BY 1,2
    ORDER BY 1
```

[Link to Query](https://app.flipsidecrypto.com/velocity/queries/9397f128-dec9-47d7-9438-db734d429bf5)

Because we are grouping by `platform` we can compare these metrics directly with some visualizations.

* [Weekly Active Wallets](https://velocity-app.flipsidecrypto.com/velocity/visuals/b479975a-8338-4b26-862e-570a54c06525/9397f128-dec9-47d7-9438-db734d429bf5)
* [Total Weekly Transactions](https://velocity-app.flipsidecrypto.com/velocity/visuals/fc920d68-98de-4c8e-b11f-18f9f8b71819/9397f128-dec9-47d7-9438-db734d429bf5)
* [Transaction per Active Wallet](https://velocity-app.flipsidecrypto.com/velocity/visuals/61eddaf3-9924-4924-85cb-f9bd1ced2cea/9397f128-dec9-47d7-9438-db734d429bf5)

But, if we don't leave the data we may miss something. Analysis requires familiarity with the subject, domain knowledge. We can compute these metrics without having used Uniswap because the data table is cleaned and presented nicely in the form of an `ez_` table.

So, to better answer this analytical bounty, one should research their subject. Let's start by simply going to Uniswap and poking around. Their homepage is a classic landing page, so let's check the blog for recent news.

{% embed url="https://uniswap.org/blog" %}

Right away (as of August 2022), we see something of note. In two separate blog posts, "Uniswap v3" is referenced.

`select distinct platform from ethereum.core.ez_dex_swaps;`

\-> `uniswapv2` and `sushiswap`

Well that could be an issue if the question is asking about all of Uniswap, in general, and not just v2. v3 is presumably newer than v2, but does that even matter? Let's see what we can find about these two versions, starting with what Uniswap itself provides.

{% embed url="https://info.uniswap.org/#/" %}

The current stats page shows... >4bn TVL and >1bn in 24h volume. Seems like a lot but we'd need to look at some relative figures to get a feel for that. There's a link on this page for [v2 Analytics](https://v2.info.uniswap.org/#/), seems like a good place to check.

... 1.5bn TVL, pretty good, and ... <100mm in 24h volume. That's a lot less.

So, our clean `ez_` table above is missing almost all of Uniswap's volume! Could we have found this out in advance? Let's check the docs:

_"This table currently contains swap events from the `fact_event_logs` table for Uniswap V2 and SushiSwap, along with other helpful columns including an amount USD where possible. Other dexes coming soon!"_

Ok, probably. So how do we get Uniswap v3 data for our analysis? Well, the docs for the `ez_dex_swaps` table says the Uni v2 and Sushi data is coming from `fact_event_logs`, so that may be a good place to start!

`select * from ethereum.core.fact_event_logs where ...`&#x20;

This is where it can get confusing - what should you look for, here?&#x20;

We can always search Etherscan for "Uniswap" and see what comes up under tokens and labeled addresses. But, fortunately and unfortunately, there are a lot of contracts out there. The dimensional labels tables are an option, but again. Lots in there, too.

So, let's get directly to the point - the activity to be modeled out is a swap. So, let's look at a swap. Interacting with a protocol is not only a great way to learn how it works, but it also creates some sample data you can investigate.

{% hint style="warning" %}
It cannot be stressed enough, but always be careful about the webpage you are on. Verify that the Uniswap you are about to connect to is the legitimate protocol. Anyone can buy an ad on Google and phishing is all too popular amongst scammers.
{% endhint %}



Anyway, here's a swap transaction we will use to find other such activity.

[https://etherscan.io/tx/0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3](https://etherscan.io/tx/0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3)

Open this transaction in Etherscan and in the `fact_transactions` table. Find where the same data is represented on both sources & start to get familiar with the elements of a transaction.
