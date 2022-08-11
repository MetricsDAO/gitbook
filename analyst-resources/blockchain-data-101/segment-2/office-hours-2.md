---
description: >-
  A recap of Week 2 Office Hours (August 10th, 2022) is below. Join live Office
  Hours weekly on Wednesdays 7-8pm ET on MetricsDAO Discord, for the duration of
  the course.
---

# Office Hours 2

### General Data Questions

#### Q: Is there a data dictionary?&#x20;

A: Not a data dictionary per se, but when you are in the [Flipside Crypto data interface](https://app.flipsidecrypto.com/), you can view the descriptions of variables. Click on a table to open the list of variables it contains. Hovering over each table field and reading provided descriptions is a good approach to explore and understand what data exists in these tables:

![](<../../../.gitbook/assets/Screen Shot 2022-08-11 at 10.55.13 AM.png>)

#### Q: Why are some fields in the tables in JSON format? (Long unparsed strings.)&#x20;

A: This has to do with how on-chain data is automatically encoded and decoded. This is the case for several blockchains, e.g. EVM-based chains, Solana, etc., and may be more computationally efficient for the blockchain to encode it in this way. To make data more human-readable for analysts, data curators (e.g. the [Data Curation pod](https://docs.metricsdao.xyz/data-curation/data-curation) on MetricsDAO) work to parse long JSON strings into separate columns, in an ongoing process to cover more tables & chains. In the way of automation, IDLs on Solana can also decode strings.

#### Q: Do Flipside table-relationship graphs exist in any other format in addition to Lineage Graphs (see [Office Hours 1 recap](https://docs.metricsdao.xyz/analyst-resources/blockchain-data-101/segment-1/office-hours-1#q-is-there-a-diagram-showing-relationships-primary-and-foreign-keys-between-separate-data-tables-e.g))? E.g. Field level graphs?&#x20;

A: Flipside is working on visuals that show how Primary Keys (PKs) and Foreign Keys (FKs) connect different tables. A primary key in a table is used to uniquely identify each record in the table; it is a field that has unique values and cannot contain NULL values. A foreign key is a field in a table that’s a primary key for another table. [Here](https://www.geeksforgeeks.org/difference-between-primary-key-and-foreign-key/?ref=lbp) is a resource to learn more about PKs vs. FKs.

#### Q: Are old Terra (1.0) tables alive?&#x20;

A: The Terra 1.0 chain is halted so there is no new data, but the backdated data exists on Flipside Crypto (check the `flipside_prod_db` schema). Terra 2.0 data will soon be processed by MetricsDAO.

#### Q: When will course participants be ready to solve analytics bounties?&#x20;

A: You can already begin exploring the [active and past bounties](https://metricsdao.notion.site/metricsdao/Bounty-Programs-d4bac7f1908f412f8bf4ed349198e5fe) in the MetricsDAO bounty program! As of August 11th, there is currently an ‘_Easy_’ level Aave bounty that you can check out if you feel like diving deeper with your learning (although the ‘_levels_’ experience is not necessarily universal, and it’s completely ok if this bounty looks hard right now).&#x20;

You can also begin exploring other analysts’ past bounty submissions – building in public and open-source analytics are very valuable for learning.

From next week, the course curriculum will take a closer look at how to solve analytics bounties, to help you with getting more into Learn2Earn!

### SQL Questions

#### Q: To aggregate the number of transactions for a time period with SQL, should I use `count` or `sum`?&#x20;

A: Use the count function! Don’t forget to add `distinct`. Example:&#x20;

```sql
select 
  count (distinct tx_hash) as txs 
from ethereum.core.ez_nft_sales 
where date(block_timestamp) between ‘2022-08-01’ and ‘2022-08-06’;
```

#### Q: When you query timestamps with `between`, does it include the final date and which timestamp?&#x20;

A: `Between` is inclusive on both sides (the first timestamp of first date, and last timestamp of last date). Try it yourself; for example see the top result of this query to see the latest included timestamp:

```sql
 select 
   block_timestamp 
 from ethereum.core.ez_nft_sales 
 where date(block_timestamp) between ‘2022-08-01’ and ‘2022-08-06’ 
 order by block_timestamp desc 
 limit 10;
```

#### Q: Could you explain the exact syntax and structure of query to find unique active wallets (from Segment 1)? Why does \`distinct\` have to include parentheses?&#x20;

A: Your query will need to begin with, for example: `select distinct(nft_from_address)` if you would like to see the records, or `select count(distinct nft_from_address)` if you are looking to count the number of addresses. Parentheses with `distinct` have to do with the compiler processing your SQL and putting bounds on your select statement.

#### Q: Could you share some tips for question #8 in Quiz 2: How many addresses does the \`dim\_labels\` table contain?&#x20;

A: The syntax for unique values is `distinct`, you can use the `count distinct()` to count unique values of a field. `Distinct` is the syntax you will always need to use when looking for unique values.

#### Q: How to select specific Ethereum address(es) in a query?&#x20;

A: Use `where [address_variable] = lower(‘address’)`. The cast to lowercase function is necessary in Flipside because their tables contain only lowercase addresses and are case-sensitive, while if you first find the address on Etherscan, for example, it may include a mix of lower- and uppercase characters.

#### Q: How can I find the biggest NFT transactions that took place?&#x20;

A: For example:&#x20;

```sql
select 
  buyer_address, 
  price_usd,
  tx_hash 
from ethereum.core.ez_nft_sales 
where date(block_timestamp) between ‘2022-08-01’ and ‘2022-08-06’ 
  and price_usd is not NULL 
  and platform_name = ‘platform’
order by price_usd desc 
limit 10;
```

To look up several platforms, alternatively you can use:`platform_name in (‘platform1’, ‘platform2’, ‘platform3’).`&#x20;
