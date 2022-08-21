---
description: A recap of Week 3 Office Hours (August 19th, 2022) is below.
---

# Office Hours 3

#### Q: Tips for solving the Educational practice bounty # 1&#x20;

A: For this bounty, you will need to decode the `tx_json` field in the fact tables, in order to find the contract address with which the transaction interacted.&#x20;

The live course session discussed how to extract the contract address from `tx_json` in Ethereum tables. Below is a syntax example of how to do it on Polygon tables.&#x20;

The below query does this for one sample transaction. You can modify your query’s WHERE clause to find the data you are looking for, e.g. specific DEX contract addresses, date range, etc.&#x20;

(_Hint_: To view more easily which fields `tx_json` contains, for example when you are looking for other pieces of information in it in addition to the contract address, you can copy the JSON from one sample record (row), and use a site that makes JSON more human-readable, e.g. _Jsonviewer_.)

```sql
SELECT tx_json:receipt:logs[1]:address 
FROM polygon.core.fact_transactions 
WHERE tx_hash = 
LOWER('0xbf3c19fc31cf921085bac089053cf611629d4fbc6002a18eb0da710a8b0ae5be')
```

#### Q: Tips for solving the Educational practice bounty # 2 (one of the possible approaches to this question)&#x20;

A: One approach can be to use CTEs to find NFT projects’ first mint dates, and then only look at projects where minting began within a recent period of your choosing, e.g. over the past week:

```sql
WITH launch_date AS ( 
  SELECT 
    min(block_timestamp) AS first_tx_date, 
    project_name 
  FROM ethereum.core.ez_nft_mints 
  GROUP BY project_name 
), 

new_projects AS ( 
  SELECT project_name 
  FROM launch_date 
  WHERE first_tx_date between '2022-08-11' and '2022-08-18' 
) 

SELECT 
  project_name, 
  COUNT (DISTINCT tx_hash) AS unique_mint_txs 
  /* , [add project metrics that you are interested in for your analysis:
      e.g. number of mint transactions, number of minter addresses, 
      amount spent, gas, number of tokens (token_id) minted] */   
      
FROM ethereum.core.ez_nft_mints         

WHERE project_name in (SELECT DISTINCT project_name from new_projects) 
      /* AND [insert any filters you are interested in, 
            e.g. block_timestamp::date between, project_name is not null, etc.] */   
                        
GROUP BY project_name 

ORDER BY unique_mint_txs /* [or instead choose one of your other metrics of interest
          from the select statement: e.g. volume of eth or usd spent, etc.] */ DESC

/* optional: limit the number of results e.g. LIMIT 10 */          
```

#### Q: For Educational practice bounty #2, how can I isolate NFTs of by project (e.g. Uniswap NFTs, other NFTs)?&#x20;

A: The first note is that Uniswap NFTs are not quite the same (by purpose) as art or utility NFTs, although they exist within the same token standard. NFTs in DeFi can represent the assets a user provides to the protocol, e.g. their position in a Liquidity Pool.\
As for the SQL to find NFT mints by project, you can use syntax similar to this (also seen in the previous query above):

```sql
GROUP BY project_name 
ORDER BY [number of mints, volume of mints, or another metric] DESC
```

#### Q: How to figure out what is a good portfolio for a beginner (e.g. NFTs)?&#x20;

A: Learning SQL and blockchain data tools can go a long way for doing your own research! When you use data sources like Flipside, you can do highly customized analysis. There are existing NFT sites too, for example HelloMoon.io for Solana NFT stats, but their charts are not interactive nor customizable, while doing your own analysis can give you interactive charts and custom insights.
