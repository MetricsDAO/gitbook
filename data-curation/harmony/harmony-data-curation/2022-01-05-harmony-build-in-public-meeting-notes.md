---
description: >-
  Targeting Jan 15th for core table development completion, next call planned
  for 2022-01-12 7:30 PM EST (please note the 1 hr shift back next week week)
---

# 2022-01-05 Harmony Build in Public Meeting Notes

**Attendees:**  forg#9122, hfuhruhurr#8781, chuxin.eth (nosugar#1554), MasterChETH#6807, BinhaChon#004, ant#8260, danner.ust#7297, kate\_chain #5152

Shoutout to the team for continuing to show up, contribute and collaborate!

<mark style="color:green;">**No blockers were identified at this time for the January 15th target completion date.**</mark>&#x20;

**General Updates from bootstrap support team:**

* j1mmy#3666 to review table progress and update permissions to allow chuxin.eth and ant#8260 to merge without slow downs
* Aiming to get more folks involved with dbt cloud to help schedule runs&#x20;

**Blocks :** [**https://github.com/MetricsDAO/harmony\_dbt/issues/2**](https://github.com/MetricsDAO/harmony\_dbt/issues/2)****

* Next step is to split into separate yml files then will be ready to merge

**Transactions :** [**https://github.com/MetricsDAO/harmony\_dbt/issues/1**](https://github.com/MetricsDAO/harmony\_dbt/issues/1)****

* Moved ticket to in progress. This is a great ticket to view as a template for schema design documentation within the comments
* Native\_from\_address is the native Harmony address vs other to & from are ETH
* Tx\_id v Tx\_hash naming being voted on in contributors discord channel
  * once decided ensure other fields match for consistency

**Logs :**  [**https://github.com/MetricsDAO/harmony\_dbt/issues/3**](https://github.com/MetricsDAO/harmony\_dbt/issues/3)

* forg#9122 taking over development of Logs, synced with hfuhruhurr#8781 for pass off already
* Transfer event name in Logs, look for any chainwalk cases where there is a native transfer. Look at logs for that transfer event name
  * Dune and Flipside tables are available as guides
  * chuxin.eth, MasterChETH#680 & ant#8260 available to partner as needed

**Transfers :** [**https://github.com/MetricsDAO/harmony\_dbt/issues/4**](https://github.com/MetricsDAO/harmony\_dbt/issues/4)****

* dependent on Logs for full build, can use Flipside Terra Transaction as a guide in interim (see comment in ticket)

<mark style="color:green;">**Next call planned for 2022-01-12 at 7:30 PM EST**</mark> for those who are able to make it. Please reach out to us in the channel to sync ahead of this time if anyone feels the January 15th target is not doable.&#x20;

****
