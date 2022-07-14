# 2022-01-19 Harmony Build in Public Meeting Notes

**Attendees:**  forg#9122, ant#8260, chuxin.eth, MasterChETH#6807, BinhaChon#004, katechain #5152, Ovix (+,+) (Welcome!)&#x20;

#### **Questions surfaced:**&#x20;

* [ ] With Harmony bounty being announced to support the Harmony Insights Dashboard ([https://talk.harmony.one/t/harmony-insights-dashboard-via-metricsdao/9607](https://talk.harmony.one/t/harmony-insights-dashboard-via-metricsdao/9607)), what level of table aggregation do we want this group to provide?&#x20;
  * Gold, silver, bronze table structure?
  * Staging tables?&#x20;
* [ ] How should python scripts be run? Will virtual machines be setup?&#x20;
* [ ] Hourly price data, is CoinGecko the best source to be using? (see HRC20 below)

**HRC20:** [https://github.com/MetricsDAO/harmony\_dbt/issues/14](https://github.com/MetricsDAO/harmony\_dbt/issues/14)

* MasterChETH working on ticket
  * able to pull, get prices into data frame and write into Snowflake&#x20;
    * will confirm timestamps look good
  * plan to use CoinGecko data for hourly price data&#x20;
    * are there any other sources we should be considering?&#x20;

### Available tables for new & existing contributors to work on thanks to Ant creating:&#x20;

**Table: Swaps #22:** [https://github.com/MetricsDAO/harmony\_dbt/issues/22](https://github.com/MetricsDAO/harmony\_dbt/issues/22)

**Table: metric\_daily\_transactions #28** [https://github.com/MetricsDAO/harmony\_dbt/issues/28](https://github.com/MetricsDAO/harmony\_dbt/issues/28)

**Table: metric\_daily\_erc20\_transfers #29** [https://github.com/MetricsDAO/harmony\_dbt/issues/29](https://github.com/MetricsDAO/harmony\_dbt/issues/29)

**Table: metric\_daily\_unique\_users #30** [https://github.com/MetricsDAO/harmony\_dbt/issues/30](https://github.com/MetricsDAO/harmony\_dbt/issues/30)&#x20;

**Table: metric\_daily\_gas\_used #31:** [https://github.com/MetricsDAO/harmony\_dbt/issues/31](https://github.com/MetricsDAO/harmony\_dbt/issues/31)

Reach out to Kate\_chain if interested in data curation!

<mark style="color:green;">**Next call planned for 2022-01-26 at 6:30 PM EST**</mark> for those who are able to make it.
