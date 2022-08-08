---
description: >-
  Office Hours take place weekly on Wednesdays 7-8pm ET on MetricsDAO Discord
  for the duration of the course. Below is the recap of the first office hours
  (August 3rd, 2022):
---

# Office Hours 1

### Data Questions

#### Q: Will this course only cover Ethereum tables, or will it also look at other chains?&#x20;

A: This course is focused on Ethereum data, as its `ez_` tables especially are more beginner-friendly.

#### Q: Is analytics knowledge specific to each blockchain?&#x20;

A: This knowledge is transferable! Familiarity with one blockchain’s data can give you many insights on how to understand the data for other chains. One example is: approaches like decoding transactions by unpacking JSON columns can work for a variety of chains.

#### Q: What are the pros and cons of using different data sources? For example, using Dune and Flipside vs. Etherscan or other APIs directly, vs. secondary analytics tools like Nansen?&#x20;

A: These approaches to accessing on-chain data vary in:&#x20;

* the flexibility to do custom work&#x20;
  * e.g. Nansen provides limited opportunities for customization
  * Flipside and Dune offer more freedom than that&#x20;
  * and using an API (from Etherscan or another source) or SDK (like Flipside Crypto’s ShroomDK) allows you to build any custom way you wish to analyze and display the data&#x20;
* the amount of data you can get before the query times out
* skills required (e.g. querying the Etherscan API can be a bit like making your own database!)
* time, ease and efficiency (Flipside is one of the great go-to places to make a quick-turnaround analysis, especially if using `ez_` prefix tables).

Premade or non-custom analytics services (like Nansen, even its free tier) can provide a great starting point for your own deeper analytical inquiry! If an existing dashboard leaves you wanting to know more – you can dive deeper on Flipside and Dune on your own. The more you dive into data, the more questions you may start to have and want to answer 😃

#### Q: I tried exploring Dune tables, and they can be quite different from the way Flipside tables are structured.&#x20;

A: The first 3 sessions of this course will be focused on Flipside `ez_` tables as they are considered beginner-friendly. But the 4th session will invite a Dune expert to dive deeper into analysis using Dune data. In the meantime, feel free to explore Dune [docs](https://docs.dune.com/) and their [top dashboards](https://dune.com/browse/dashboards).

#### Q: What is your take on identifying bot clusters and how to filter them out in the dataset?&#x20;

A: This can depend on the questions your analysis is after, the chain you are analyzing, etc. One threshold recommended by Anduril is “15 transactions in 30 min” for a bot. But largely, this depends on your thesis/hypothesis and what you want to accomplish with your analysis: perhaps find NFT bots, or ones that spam transactions, etc.

#### Q: Do you have any tips on working with SQL on Gnosis Safe data?&#x20;

A: A good starting point is to start with the basics and build up on that, as well as look into the documentation for the relevant project(s). A good place to start exploring blockchain data is also to copying a transaction ID and dissect how this transaction shows up in different tables.

#### Q: How to go farther back in time for analytical questions where you want to look at historical data?&#x20;

A: This can be an advanced topic! A starting point can be to explore relevant documentation and available APIs and SDKs.

#### Q: Is there a diagram showing relationships (primary & foreign keys) between separate data tables (e.g. in Flipside)?

A: (Updated on August 8, 2022) Currently, Flipside table relationships can be explored by accessing their _dbt_ data models => Lineage Graph view. While Lineage graphs can look complex, they provide insight into relationships between tables.

* In Flipside Crypto's data [documentation](https://docs.flipsidecrypto.com/our-data/tables), you can find the blockchain table(s) you are interested in, and follow the link for that chain's Flipside data model.&#x20;
  * E.g. the Ethereum tables [docs](https://docs.flipsidecrypto.com/our-data/tables/table-schemas) will link to the Ethereum [dbt data model](https://flipsidecrypto.github.io/ethereum-models/#!/overview/ethereum\_models).
* Select a table from the dbt docs' left-side menu. A teal circle in the bottom right corner will open a Lineage Graph that illustrates between-table relationships.

### SQL Questions

#### Q: What date or time methods can be used with the `block_timestamp` string?&#x20;

A: A best practice would be to use `where date(block_timestamp) between ‘yyyy-mm-dd’ and ‘yyyy-mm-dd’` syntax.&#x20;

`block_timestamp::date` is another alternative.&#x20;

As for syntax like ILIKE, it technically works, but is intended for strings rather than the datetime format.&#x20;

Using the entire `block_timestamp` variable without excluding hours, minutes, seconds can yield slightly different results (over/undercounting) compared to the the first two methods above.

#### Q: Why are there rows in the `ez_nft_sales` table where `event_type` is blank/null/unknown?&#x20;

A: An exploratory query reveals that this may only be the case for sales on Rarible. _You can also try writing your own query_ to explore this data quirk, filtering by `where event_type is NULL`

#### Q: Any tips on how to use the `date_trunc` method?&#x20;

A: `date_trunc` helps select what part of block timestamp you would like to look at: day, hour, week, etc. More details can be found in the [documentation](https://docs.snowflake.com/en/sql-reference/functions/date\_trunc.html) (referenced here are Snowflake docs because Flipside runs on Snowflake, but you can also explore other sources of documentation for this method).&#x20;

#### Q: What is a “successful” NFT sale in the data? (In reference to the quiz question).&#x20;

A: This would be more applicable if the `ez_nft_sales` table contained a `status` (success/fail) column.&#x20;

_If you are looking to dive deeper_: why not test out with your own query? Try discovering whether the `ez_nft_sales` table contains only successfully executed transactions, or whether some of these transactions might have failed. (_Hint_: Both the `ez_nft_sales`and the `fact_transactions` Ethereum tables on Flipside contain the transaction hash column, and the latter table has a `status` column for transaction success/fail.)

#### Q: What are Common Table Expressions?&#x20;

A: A Common Table Expression (CTE) is “a table within a table”, and can be combined with the join/union methods to produce more complex queries. _For those who feel like exploring this more advanced topic_ – here is a documentation [link](https://docs.snowflake.com/en/user-guide/queries-cte.html).

### Useful Tips, Reminders, and Suggestions

#### Q: A tip for the Quiz #1 question on DEX swaps:&#x20;

A: Filtering by platform name (e.g. Uniswap v2) is recommended: this will ensure that the query is catching all transactions of interest in this question. In contrast, if you manually try to identify individual pool names that are relevant for this question, it may result in missing some**.**

#### Q: A note on the Quiz #1 question on NFT sales:&#x20;

In this question, it is important to filter by event type, to only look for sales.

#### Q: My query is taking a long time to run.&#x20;

A: Remember the importance of filtering queries (e.g. limit by date range) to help them run quicker!

#### Q: Briefly, what is the plan for the course content going forward?&#x20;

A: The plan is an incremental increase in difficulty! Going forward, the course will level up the SQL skills that learners began to build in Session 1/Week 1. You will also learn how to create data visualizations.

### Bounties: Getting started with Learn2Earn

#### Q: What are blockchain analytics bounties?&#x20;

A: A good way to apply your newly learned on-chain data skills is to solve some bounties! By completing bounties, you will produce analytics and have a chance to earn some crypto. Beginner-level bounties can be a good place to start.&#x20;

* [MetricsDAO bounty program](https://metricsdao.notion.site/metricsdao/Bounty-Programs-d4bac7f1908f412f8bf4ed349198e5fe) and [Past great submissions](https://metricsdao.xyz/showcase)&#x20;
* [Flipside Crypto bounty program](https://flipsidecrypto.xyz/earn) and [Past great submissions](https://flipsidecrypto.xyz/discover/dashboards?project=ALL\&sort=new\&isGrandPrize=true\&date=All\&user=)

### Where can I join the next Office Hours?

Join us on MetricsDAO [Discord](http://discord.gg/metrics) Wednesdays at 7pm ET for the duration of the course. Check the Events tab and the [#course-faq](https://discord.com/channels/902943676685230100/996143485390426162) channel for the upcoming Office Hours event link.

### Feedback

Have any feedback you have on the course, quizzes, office hours, etc.? Share it on [Discord](http://discord.gg/metrics) ([#course-chat](https://discord.com/channels/902943676685230100/992490932412883064) channel)!
