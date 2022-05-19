---
description: Recap of topics covered in the first Harmony Data Curation contributors call
---

# 2021-12-10 Harmony Build-In-Public Meeting Notes



**Introductions** from BinhaChon#0041, hfuhruhurr#8781, nosugar#1554, MasterChETH#6807, forg#9122, j1mmy#3666, danner.eth#7297 & kate\_chain #5152 &#x20;

A walk-through of what **j1mmy#3666** has been building for MetricsDAO as part of the white glove bootstrap support Flipside Crypto has been providing.&#x20;

![MetricsDAO Stack: Bootstrap support provided by Flipside Crypto](../../../../.gitbook/assets/image.png)

{% content-ref url="../../analytics-stack/" %}
[analytics-stack](../../analytics-stack/)
{% endcontent-ref %}

**Phase 1: DBT Models to be built**&#x20;

DBT uses Jinja templates for generating the sql statements that create the tables in Snowflake. Harmony DBT DEV environment is available so you can run commands locally and write to Snowflake.

**Header** field in Blocks and TXS contains a JSON with data that is unique to the Harmony chain. This is the data we need to break out into additional fields.&#x20;

As we produce tables we can document with a schema.yml file and define it like the source. The documentation site can be built to the main page of the repo so any user could see that.

| Table Name   | Notes                                                                                                                                                          | Lead & Reviewer                               |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| Blocks       | Started, needs more fields & Harmony refinement                                                                                                                | see [Broken link](broken-reference "mention") |
| Transactions | Transactions can be between any 2 parties (does not need to be a transfer of value, could be interacting with a smart contract) ‘these 2 addresses interacted’ | see [Broken link](broken-reference "mention") |
| Logs         | EVM, every transaction has a receipt with logs that gets emitted. Calling a contract and it transfers between several different contracts it’s all in the logs | see [Broken link](broken-reference "mention") |
| Transfers    | Can pull from top level transactions and logs                                                                                                                  | see [Broken link](broken-reference "mention") |

**Phase 2: DBT Models**

| Table Name    | Notes | Builder (discord handle) |
| ------------- | ----- | ------------------------ |
| Defi\_Kingdom |       |                          |

**dbt Resources :**[ **dbt Video Tutorials**](https://www.youtube.com/playlist?list=PLy4OcwImJzBLJzLYxpxaPUmCWp8j1esvT)**,** [**dbt Courses**](https://courses.getdbt.com/collections)**,** [**dbt Style Guide**](https://github.com/dbt-labs/corp/blob/master/dbt\_style\_guide.md)****

If using vscode, 2 extensions are recommended: dbt formatter & dbt power user

**Next Steps**

1. Reach out to j1mmy#3666 for Snowflake account and to share GitHub username to be added to MetricsDAO&#x20;
2. Digest materials and reach out to kate\_chain #5152 if you'd like to focus on a table outlined above
3. Meet same time next week in Build-In-Public! 2021-12-17 6:30 PM EST&#x20;
