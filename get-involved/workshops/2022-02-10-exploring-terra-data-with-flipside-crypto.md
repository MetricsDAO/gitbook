---
description: 'Mentor''s Workshop #2'
---

# 2022-02-10 Exploring Terra Data with Flipside Crypto

## Recording

{% embed url="https://www.youtube.com/watch?v=s3feVSU4Wb8" %}

## Resources

We've created a new page under the Mentor's Circle GitBook! Resources we find helpful and that are referenced in the MetricsDAO Workshops will be added to an ever-expanding repository.

{% content-ref url="../operational-pods/mentors-circle/resources.md" %}
[resources.md](../operational-pods/mentors-circle/resources.md)
{% endcontent-ref %}

## Follow Along with Starter Queries!

Feel free to Copy & Edit and make them your own!

### 0 - Exploring the Data

[MDAO Workshop - Anchor Collateral Starter Query 0](https://app.flipsidecrypto.com/velocity/queries/572039b9-5864-4b41-9164-fc2294fb8866)

Start by running a simple `SELECT` statement so we can see the data in the `anchor.collateral` table. When using `SELECT *` from a table for this purpose, **always** use a [`LIMIT`](https://mode.com/sql-tutorial/sql-limit/).

### 1 - Collateral Transactions

[MDAO Workshop - Anchor Collateral Starter Query 1](https://app.flipsidecrypto.com/velocity/queries/aa3eb6c6-6cd6-42e4-b7d2-97c72aae3b0b)

Using this query, we take a high level view of the collateral transaction volume happening with Anchor Protocol.

We're using a few SQL techniques here to aggregate data and look at trends across time. As mentioned in the workshop, the initial goal is to take a look at general trends so transaction volume, simply by count of collateral adds or withdrawals, each day is where we are going to start.

To do that we need to combine all data from a day into one number, so we use [`date_trunc()`](https://docs.snowflake.com/en/sql-reference/functions/date\_trunc.html) to flatten all timestamps from throughout the day into one, common, date. Then, we use the [aggregation function](https://mode.com/sql-tutorial/sql-aggregate-functions/) `count()` to simply count up the number of records associated with that day.

When using an aggregate function, we need to tell SQL what the "groups" are. In this case, we are going to [`group by`](https://mode.com/sql-tutorial/sql-group-by/) the date that was calculated above, with `date_trunc()`.

Finally, let's order the data by day using [`order by`](https://mode.com/sql-tutorial/sql-order-by/). Flipside's charting tool will generally automatically do this, but it's good practice.

#### Additional tables from the workshop:

* [Data Check](https://app.flipsidecrypto.com/velocity/queries/0389886a-fdae-4055-99e1-e726c6cef9e1) using [`distinct`](https://mode.com/sql-tutorial/sql-distinct/)
* [Gross Collateral Transaction Events](https://app.flipsidecrypto.com/velocity/queries/63767222-e809-4b9a-bb78-20b5138326c6)
* [Collateral Transaction Events, bLUNA](https://app.flipsidecrypto.com/velocity/queries/a0075801-3555-4978-b5cb-ee98c1e6612d) using [`where`](https://mode.com/sql-tutorial/sql-where/)``
* [Collateral Transaction Events, bETH](https://app.flipsidecrypto.com/velocity/queries/7fa0643a-f208-4542-a17e-275d40ee8ab6)

### 2 - Transaction Volume

[MDAO Workshop - Anchor Collateral Starter Query 2](https://app.flipsidecrypto.com/velocity/queries/274db57c-8805-49bd-b118-5a39d5f8f43b)

Using the techniques learned above, let's determine the gross volume of collateral, in USD, for these transactions. This utilizes the [`sum()`](https://mode.com/sql-tutorial/sql-sum/) aggregate function.

The `amount_usd` column is a computed value by the Flipside team. When working with these, always check for missing values. [Checking for Null Values in amount\_usd](https://app.flipsidecrypto.com/velocity/queries/cd221ed5-5bdc-4696-8997-79cdb9530cb5). From this query we see that there are a few dates with significant missing data. Accounting for missing data is beyond the scope of this workshop, but checking the quality and completeness of the data tables is essential to good analysis. This should be noted in our final dashboard.

#### Additional tables:

* [MDAO Workshop - Anchor Collateral Volume - Gross by event](https://app.flipsidecrypto.com/velocity/queries/7afdb980-6c36-42aa-84a8-61790c5cc63f)
* [MDAO Workshop - Anchor Collateral Volume - Gross by Collateral](https://app.flipsidecrypto.com/velocity/queries/e680cc97-3595-45ec-8b2d-eb3b99f6c193)

### 3 - User Behavior

[MDAO Workshop - Anchor Collateral Starter Query 3](https://app.flipsidecrypto.com/velocity/queries/50936448-72ff-400b-a3c1-e72bd81e20ab)

High level volume is a useful starting point, but transaction count and USD volume flows only tell us so much. What are users doing and how is that changing across time? We can compute some powerful summary statistics using the same exact techiques.

Replace `count()` or `sum()` with [`avg()`](https://mode.com/sql-tutorial/sql-avg/) in the aggregation, and we start to see trends emerge.

Outliers should be investigated, and we can do a couple things about those. First, let's figure out why average bETH is spiking by finding the top transactions, by `amount_usd`.&#x20;

[Query Here](https://app.flipsidecrypto.com/velocity/queries/90157f8a-179d-4a32-bc13-5090dceb08df)&#x20;

We use `order by` to specify which column and `desc` to ensure the highest numbers are ordered at the top. As with above, we need to exclude `null` values using [`where amount_usd is not null`](https://mode.com/sql-tutorial/sql-is-null/). Again, set a `limit`! We only need the top few results.

[`median()`](https://docs.snowflake.com/en/sql-reference/functions/median.html) is another aggregate function that we can use to interpret user behavior. Averages tend to be skewed as the [`max()`](https://mode.com/sql-tutorial/sql-min-max/) continues to grow, so this provides us with valuable insight into what the more "average" user is doing.

#### Additional tables:

* [MDAO Workshop - Anchor Average Transaction, by Collateral](https://app.flipsidecrypto.com/velocity/queries/b75736c7-82db-44ec-87f7-d9e4d25edae0)
* [Average Transaction, excl Outliers](https://app.flipsidecrypto.com/velocity/queries/d6b6194c-f8c6-401d-a79b-d0238e36c221)
* [Median Transaction Size](https://app.flipsidecrypto.com/velocity/queries/61f856aa-f0ba-4733-aa6d-35c17fcf41b9)
* [Median Transaction, by Collateral](https://app.flipsidecrypto.com/velocity/queries/5c1c94e6-b13e-4605-a7d6-dc8967efe30e)

### Final Product - the Dashboard

{% embed url="https://app.flipsidecrypto.com/dashboard/metrics-dao-workshop-2-Vh9_IN" %}
Final dashboard using our queries from above.
{% endembed %}

Key points about the final product, describe the data! What insights do you see? What was interesting along the course of the investigation. Write-ups do not need to be long, by any means, but telling the story of the data is very important.
