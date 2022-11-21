---
description: >-
  MetricsDAO follows dimensional modeling standards. Guidelines and requirements
  are laid out below. Curated models must adhere to this guide for final
  approval to merge.
---

# Data Modeling Standards

At Flipside there are many public schemas with the majority being data curated tables that are from the blockchain, including the **Harmony** and **NEAR** data curated by the MetricsDAO community. There are some that are other types such as metadata for labeling and informing across chains. In order to have analysts, from the novice user to the skilled analyst, be delighted by data, there needs to be a shared standard across the data organization on how data is curated and presented to the end user. The star schema is a mature modeling standard optimized for analytical use.

## General Resources

Our general model and style standards are derived from the best practices guide put forth by dbt Labs:

{% embed url="https://github.com/dbt-labs/corp/blob/main/dbt_style_guide.md" %}

All code that is submitted for a PR should be formatted according to [this dbt autoformatter](https://github.com/henriblancke/dbt-formatter), available as an extension on the VS Code extension marketplace.

## Table Layers

### Bronze

1. Blockchain data that has been indexed and piped into Snowflake under `chainwalkers` schema. This includes all core data characterizing what occurs on a chain (e.g. blocks, transactions, function calls, state changes, etc). Chainwalkers 2.0 decodes log data, but does no other transformation.&#x20;
2. The only data that has been added to this is `_ingested_at` and `_inserted_timestamp`. This has been added a requirement for all blockchains for efficiency and data integrity reasons.
3. Any ingested data should be in the bronze layer.
4. This layer is a view on the source, as such it is the only layer where `{{ source() }}` should be called and no transformations shall happen in bronze.

### Silver

1. Filtered, cleaned and transformed data.
2. Silver models should de-duplicate bronze, as chainwalkers may re-ingest a block at a later date.
3. The models in this layer are incremental as to reduce compute time and cost.
4. Fact and dimension tables which are completely decoded (where we can), are additive (no replacing data), deduped, have not been joined to other tables. We can expose silver tables in the public facing app as a gold view.&#x20;
5. Can be a combination of data sources.

### Gold (Core)

1. Curated models exposed to the public front-end.
2. [Fact and dimension](https://docs.google.com/document/d/1sdtchIcnkzMyP0HLQkA-c3BtE4AWgNFjiGFnhX3YzAs/edit#heading=h.snh3fvv82vz1) tables should never be combined in tables ie: no joining transactions and labels. They can be combined in views, where the logic is done in the underlying queries.&#x20;
3. Views that can ease the burden for analysts. The wide array of data-users include some new to SQL, new to analytics, and/or new to blockchain technology. Incorporating off-chain metadata, and even aggregations (e.g. daily summaries of key transactions) can help new users understand the ecosystem as a whole.&#x20;
   1. This also eases the burden on the underlying systems, and facilitates “Easy” bounty programs.&#x20;
   2. Facilitates learning for new users.
   3. Examples include: labels, transfers, event logs, swaps, liquidity provision/removal, daily balances of holders, prices and decimals, daily transfer summary.
4. Models that accelerate analytics for a particular protocol (e.g. compound, uniswapv3, anchor, mirror schemas).

## Descriptive Naming Conventions

### 3 Different Types of Tables

All tables and views should have a prefix of what type of data is within (based on [star schema](https://docs.google.com/document/d/1GxWCUBkMB55h1Qb8-t42JW7s2yJWe57nsElzE4gMSyc/edit)).

All names should\_be\_snake\_case. Abbreviations should be avoided when possible. Abbreviations should match an iso standard ie: currency or country names, etc.

1. Facts (`fact_`)
   1. Fact table contains measurements, metrics, and facts. Anything that is measurable, summing, averaging, anything over time.
2. Dimensions (`dim_`)
   1. Dimension table is a companion to the fact table which contains descriptive attributes to be used as query constraining.
3. Convenience Views (`ez_`)
   1. Convenience Views can combine facts and dimensions for reasons above. This should only be views in the gold layer.
   2. Where analytics is doing more of the “lift” for the view.

### Example of a Schema

Ethereum\_

* Fact\_
  * `fact_transactions`
  * `fact_blocks`
  * `fact_events`
  * `fact_traces`
* Dim\_
  * `dim_contract_metadata`
  * `dim_date`
* Convenience View or ez\_ &#x20;
  * For convenience views where analytics is doing a lot of the “lifting” for the view - aggregate
  * Mostly for scavenger hunts/training/level-up
  *   Examples Include:

      * `ez_balances_usd_agg_daily`
      *   `ez_dex_swaps`Descriptive Naming Conventions

          ###



## Automation

When creating models with _incremental_ materialization, we need to write an incremental logic within the model. It is important for the incremental logic to be based on _\_inserted\_timestamp_ and not on the _block\_timestamp._ This is important especially when the data encounters gaps on certain dates. This enables the model to heal itself because gaps are associated with _block\_timestamp_ and when they get-inserted later, they get captured by  _\_inserted\_timestamp._\
__Here is an example:

```
 {% raw %}
{% if is_incremental() %}
AND _inserted_timestamp >= (
    SELECT
        MAX(_inserted_timestamp) :: DATE - 1
    FROM
        {{ this }}
)
{% endif %}
{% endraw %}
```

