---
description: Filtering & ordering our results.
---

# Filter data with WHERE

## WHERE

We rarely want every record possible, however, so we'll need a way to filter the results. `WHERE` is aptly named, as it will return records where a designated condition is matched.&#x20;

Say we want to take a look at what a16z is up to in [this identified wallet](https://debank.com/profile/0x66b870ddf78c975af5cd8edc6de25eca81791de1).

```sql
SELECT 
    *
FROM ethereum.core.fact_transactions
WHERE from_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'
LIMIT 100;
```

__[_Link to Query_](https://app.flipsidecrypto.com/velocity/queries/a7720f36-890d-4f25-89c2-a8d80a5dce6a)__

According to [Etherscan](https://etherscan.io/address/0x66b870ddf78c975af5cd8edc6de25eca81791de1), this wallet has performed nearly 8,000 transactions so selecting a random set of 100 doesn't show us much. Maybe we're looking for just the 100 most recent ones. In addition to filtering data with `WHERE`, we can order the result set by a column using `ORDER BY`.

In this example, we are looking for where `from_address` matches a string by using `=`, but we can using any [comparison operator](https://mode.com/sql-tutorial/sql-operators/) following the `WHERE`, depending on what we are looking to filter.

| Equal to                 | `=`          |
| ------------------------ | ------------ |
| Not equal to             | `<>` or `!=` |
| Greater than             | `>`          |
| Less than                | `<`          |
| Greater than or equal to | `>=`         |
| Less than or equal to    | `<=`         |

## ORDER BY

```sql
SELECT 
    *
FROM ethereum.core.fact_transactions
WHERE from_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'
ORDER BY block_timestamp DESC
LIMIT 100;
```

__[_Link to Query_](https://app.flipsidecrypto.com/velocity/queries/f308e8d1-f1fd-4ca2-9050-ae2d9b5d27c7)__

We can use `ORDER BY` to organize our result set using any column. By default, `ORDER BY` will use ascending (`ASC`) order (A->Z, 0->9, past->present) unless you pass `DESC` to specify descending order (Z->A, 9->0, present->past).

{% hint style="info" %}
This slots in _after_ the `WHERE` clause and _before_ any `LIMIT`.
{% endhint %}

In the above example, we are explicitly stating `block_timestamp` but we can also refer to columns by their position. Open the linked query and we can see that `block_timestamp` is the second column, so we can, alternatively, use `ORDER BY 2` ([which is the preferred method over listing the column name](https://www.getdbt.com/blog/write-better-sql-a-defense-of-group-by-1/)).

## Logical Operators

### AND

We can filter on more than just one item, maybe we don't want the 100 most recent, but transactions since a date.

```sql
SELECT 
    *
FROM ethereum.core.fact_transactions
WHERE from_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'
    AND block_timestamp >= '2022-08-01'
LIMIT 10000;
```

or just transactions within the past few days.&#x20;

{% hint style="info" %}
#### CURRENT DATE

We can use a [context function](https://docs.snowflake.com/en/sql-reference/functions-context.html), `CURRENT_DATE` to write the `block_timestamp >=` filter to update as time progresses.
{% endhint %}

```sql
SELECT 
    *
FROM ethereum.core.fact_transactions
WHERE from_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'
    AND block_timestamp >= CURRENT_DATE - 3;
```

__[_Link to Query_](https://app.flipsidecrypto.com/velocity/queries/bdc8b3e7-daf3-4a7c-a913-bf6a2ac56538)__

### OR

We can apply another conditional operator to the where clause, trusty OR. This page, [0xilluminati](https://0xilluminati.com/34852f877c984217985a41ca23680fe2), has listed another a16z wallet address. So, let's say we want to view the transactions by both.

```sql
SELECT 
    *
FROM ethereum.core.fact_transactions
WHERE (from_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'
    OR from_address = '0xc564ee9f21ed8a2d8e7e76c085740d5e4c5fafbe')
    AND block_timestamp >= '2022-07-28'
LIMIT 100;
```

[_Link to Query_](https://app.flipsidecrypto.com/velocity/queries/57784f40-d32e-4cbb-9122-3793a5305273)__

Notice anything else different here? We have to add `(`parentheses`)` around the clause in which we want `OR` to apply. This is because, ultimately, the filter we apply to the query is still comprised of two parts, even though we are adding a new condition.

**‼️ Remember PEMDAS? Conditional logic has an order of operations, as well!**

One way to look at is the following. Each side of the table (left and right) is a side of the `AND` clause, and we only want records where both evaluate to true.

The `from_address` will evaluate to true in two instances, where it equals either of those addresses. The `block_timestamp` part of the clause evaluates to true only where the date is greater than, or equal to, July 28th, 2022.

| A                                                             | B                                 |
| ------------------------------------------------------------- | --------------------------------- |
| `from_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'` | `block_timestamp >= '2022-07-28'` |
| `from_address = '0xc564ee9f21ed8a2d8e7e76c085740d5e4c5fafbe'` |                                   |

Each logical condition does not need to refer to the same column. Say we wanted to filter transactions where `0x66b...` is either the sender or recipient. We could have something like the following, where the code would look something like `WHERE A AND B.`

| A                                                             | B                                    |
| ------------------------------------------------------------- | ------------------------------------ |
| `from_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'` | `block_timestamp > CURRENT_DATE - 7` |
| `to_address = '0x66b870ddf78c975af5cd8edc6de25eca81791de1'`   |                                      |

{% hint style="success" %}
How would this look in SQL? Try writing it out using [Flipside](https://flipside.new) or [Dune](https://dune.com/browse/dashboards).

Still confused? Take a look at [this page](https://www.bennadel.com/blog/126-sql-and-or-order-of-operations.htm) for further discussion on AND / OR.
{% endhint %}

### LIKE

Sometimes we don't know the full term (maybe it's an event/method name) or there are multiple identifiers with a commonality.

Dex swaps is an example of this, say we want to find all pools for `ENS` tokens, so we can search for that.

```sql
SELECT 
    DISTINCT pool_name
FROM ethereum.core.ez_dex_swaps
WHERE pool_name LIKE 'ENS'
LIMIT 100;
```

No results... why is that? I thought `LIKE` was supposed to look at a string (in this case, `pool_name`) and find matches that are similar to what we declare (`ENS`).

This is true, but as the code executes, it will look for exactly `ENS` and nothing more. If we want something that _contains_ `ENS`, but may have more than just `ENS` in the record than we need to use **wildcard** characters.

```sql
SELECT 
    DISTINCT pool_name
FROM ethereum.core.ez_dex_swaps
WHERE pool_name like '%ENS%'
LIMIT 100;
```

[Link to Query](https://app.flipsidecrypto.com/velocity/queries/9b33cc3c-450d-42e0-a285-c5d8e70c8add)

Great! We're done. We found all the pools in `ez_dex_swaps` that include the `ENS` token, right? Not quite, open the link to the sample query and take a look at the results. `ENS` is not just a token name, but it's also a common string of letters so we've got quite a lot of liquidity pools returning. Looking through, we do see `WETH-ENS LP` in there, so not all hope is lost! We need to do some work looking at the data in the table **in a targeted way.**

In fact, we are learning something else here - all liquidity pools returned are following a similar pattern. `token-token LP`, with `WETH` being a pretty common pair. So, let's take what we're learning with this **data exploration** and try another query, using a couple concepts learned so far:

```sql
SELECT 
    DISTINCT pool_name
FROM ethereum.core.ez_dex_swaps
WHERE pool_name LIKE 'ENS-%'
  OR pool_name like '%-ENS LP'
LIMIT 100;
```

[Link to Query](https://app.flipsidecrypto.com/velocity/queries/fd30ddc0-fab3-4686-a8c7-5797a5116335)

We know that the token we are looking for could be either the first in the pair, with additional characters following (`ENS-%`), or it's the second token in the pair and `LP` follows.

Adding `%` is far from the only way we can add a wildcard, take a look at some of these examples from [w3schools](https://www.w3schools.com/sql/sql\_like.asp):

| LIKE Operator                | Description                                                                   |
| ---------------------------- | ----------------------------------------------------------------------------- |
| `WHERE <column> LIKE 'a%'`   | Finds any values that start with "a".                                         |
| `WHERE <column> LIKE '%a'`   | Finds any values that end with "a".                                           |
| `WHERE <column> LIKE '%or%'` | Finds any values that have "or" in any position.                              |
| `WHERE <column> LIKE '_r%'`  | Finds any values that have "r" in the second position.                        |
| `WHERE <column> LIKE 'a_%'`  | Finds any values that start with "a" and are at least 2 characters in length. |
| `WHERE <column> LIKE 'a__%'` | Finds any values that start with "a" and are at least 3 characters in length. |
| `WHERE <column> LIKE 'a%o'`  | Finds any values that start with "a" and ends with "o".                       |

### IN

Sometimes, we don't need as much exploration and know exactly what pool we're looking to include. In that case, we can use `IN` to search through a list and match based on our inputs.

```sql
SELECT 
    DISTINCT pool_name
FROM ethereum.core.ez_dex_swaps
WHERE pool_name IN
    (
        'ENS-WETH LP',
  	'USDC-ENS LP',
        'WETH-ENS LP'
    )
LIMIT 100;
```

[Link to Query](https://app.flipsidecrypto.com/velocity/queries/819d2899-3537-4c22-83d6-31004a15cde0)

_The list of strings that we're looking for does not need to be spread across multiple lines like above. Further, you could use non-string values in the list as long as they type across all options is **consistent**. One could find swaps for a variety of precise swaps by using something like `WHERE amount_out_usd IN (1, 500, 10000)`_ , but the following is not legal _`WHERE <column_name> IN ('abc', 5, 'def')`._

### BETWEEN

Instead of writing something like `where date >= tuesday and date <= thursday`, we can write `where date between tuesday and thursday`.

```sql
SELECT 
    *
FROM ethereum.core.ez_dex_swaps
WHERE block_timestamp::DATE BETWEEN '2022-06-01' AND '2022-06-03'
LIMIT 100;
```

[Link to Query](https://app.flipsidecrypto.com/velocity/queries/12956021-1de3-4325-80fb-146626378811)

{% hint style="info" %}
Note the new `::DATE` added to `block_timestamp` in the where clause. This is called typecasting and what's happening here is that we are taking `block_timestamp` which is a [`timestamp`](https://docs.snowflake.com/en/sql-reference/data-types-datetime.html#timestamp) and we are changing that to a [`date`](https://docs.snowflake.com/en/sql-reference/data-types-datetime.html#date).

`BETWEEN` _is_ inclusive, but when we compare a timestamp to a date, we run into some issues. The second date is interpreted as midnight _when the day starts_.

In practice, this takes a timestamp (like `2022-08-01T14:00:00Z` or `2022-08-01T22:00:00Z`) and casts both those to just the date, i.e. `2022-08-01`.

Take a look at [this example query](https://app.flipsidecrypto.com/velocity/queries/7361f017-6f5e-4b30-a9ac-f8f49ad8ea6f) and run the where clause both ways, with and without the typecast. Notice how the result set differs?

If you _really_ want to get into the weeds with how between, timestamp, and dates interact check out [this post](https://sqlblog.org/2009/10/16/bad-habits-to-kick-mis-handling-date-range-queries).
{% endhint %}

### NOT

`NOT` can be added before any conditional statement to negate it. This is commonly used to ignore some specific known records we don't want to return.

Example: `like abc% and not in ['abcd', '1abc']`

```sql
SELECT 
    DISTINCT pool_name
FROM ethereum.core.ez_dex_swaps
WHERE pool_name NOT IN
    (
        'ENS-WETH LP',
  	'USDC-ENS LP',
        'WETH-ENS LP'
    )
LIMIT 100;
```

## Roundup

So, we have learned a lot of ways to filter data an look through the tables at the transaction level. That's great for data exploration and for finding records of a specific type. Why does this matter? (Hint: I made it bold in a sentence up above).

**Data exploration** is so important to understanding what we are analyzing and is an area we will continue to highlight.

## Dive Deeper

{% embed url="https://www.w3schools.com/sql/sql_orderby.asp" %}

{% embed url="https://mode.com/sql-tutorial/sql-operators/" %}

{% embed url="https://mode.com/sql-tutorial/sql-logical-operators/" %}

{% embed url="https://www.bennadel.com/blog/126-sql-and-or-order-of-operations.htm" %}
