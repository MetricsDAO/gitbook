---
description: Test your environment setup with an archived dataset.
---

# Onboarding Project

Note: this page is under active development and will soon include a walkthrough for curating a model, following the core steps an active curator in the pod would take to contribute to a data model.

An onboarding repository has been set up on our Github page with core models for a 3-month snippet of Harmony data. This data is represented in the databases `ONBOARDING` and `ONBOARDING_DEV` in Snowflake and can be used as a sandbox for learning the ropes.

{% embed url="https://github.com/MetricsDAO/onboarding_dbt/" %}



## Video Workshop: Data Curation and dbt

chuxin.eth ran a workshop in March 2022 on using dbt to curate tables. Feel free to follow-up with any questions from this in Discord!

{% embed url="https://youtu.be/wj_2ljFABuA" %}
Data Curation with Chuxin
{% endembed %}

## Legacy Instructions

While the new walkthrough is being written, the prior onboarding instructions will remain live below.

### Steps to start contributing:

1. Pick a task from Metrics Dao issue board:
   * Harmony: [https://github.com/MetricsDAO/harmony\_dbt/issues/](https://github.com/MetricsDAO/harmony\_dbt/issues/)
   * NEAR: [https://github.com/MetricsDAO/near\_dbt/issues](https://github.com/MetricsDAO/near\_dbt/issues)
   * Terra: [https://github.com/MetricsDAO/terra\_dbt/issues](https://github.com/MetricsDAO/terra\_dbt/issues)
2. Design the database schema or figure it out as you go depending on your style. In this working example, we will try recreating harmony.prod.blocks (\[Database].\[Schema].\[Table Name]).
   * See proposed table schema here: [https://github.com/MetricsDAO/harmony\_dbt/issues/2](https://github.com/MetricsDAO/harmony\_dbt/issues/2)
3. Start writing code in the snowflake UI to get a table.
   * You can skip to step 4-5 if you are able to start writing dbt-like SQL directly.
   * We are going to build on top of the staging table harmony.prod.stg\_blocks(see below).
   * ![](<../../.gitbook/assets/image (3).png>)
4. Convert snowflake UI code to dbt cloud code. dbt combines sql with Jinja, see more: [https://docs.getdbt.com/docs/building-a-dbt-project/jinja-macros](https://docs.getdbt.com/docs/building-a-dbt-project/jinja-macros)
   * You can copy the code directly from this file and test it out on dbt cloud: [https://github.com/MetricsDAO/harmony\_dbt/blob/main/models/core/blocks.sql](https://github.com/MetricsDAO/harmony\_dbt/blob/main/models/core/blocks.sql)
5. Copy dbt cloud code into the correct folder for the table. If you're using command line, remember to git pull (gup) from the main branch for latest updates and git checkout -b (gcb ) to create a working branch locally.
   * For this working example, you can do gcb yourname-test-blocks
   * ![](<../../.gitbook/assets/image (4).png>)
   * If you want to build the blocks table in dev, you can rename your sql file as yourname\_blocks.sql
   * ![](<../../.gitbook/assets/image (1).png>)
6. Test it using the commands make `dbt-console` and then `dbt run` to run the entire project’s models on the snowflake database (It’ll take around 30 minutes). If you only want to test your own model, you can use the command `dbt run --select your_table_name`. See highlighted commands below:
   * ![](<../../.gitbook/assets/image (12).png>)
   * Once it finishes running, you'll be able to see the table available in dev
7. Make sure your table successfully runs in the dev environment before pushing your branch. Command + D to exit Docker environment. git add all the changes you want to include in the branch, and then add git commit -m "your message". Push your branch to remote using git push or gp (follow what's suggested in the terminal if it's your first time pushing the branch to remote).
   * ![](<../../.gitbook/assets/image (8).png>)
8. If your PR is adding or changing existing models or documentation, run `dbt docs generate` as the last commit to ensure documentation updates to include your changes.
9. Create Pull Request ( [https://github.com/MetricsDAO/harmony\_dbt/compare](https://github.com/MetricsDAO/harmony\_dbt/compare) ) and write a summary on your updates/changes, as well as attaching passing test logs.
10. Request Reviewer (From one of the leaders below).
11. Fix Review Comments.
12. Re-Request Reviewer after fixing review comments.
13. If your PR has been approved, merge it to production (Production is scheduled to run every 6 hours).
14. Congratulations! You’ve successfully contributed a table to MetricsDAO.
15. Testboard \[Optional]: If you’d like to have some sort of testing
    * [https://app.snowflake.com/us-east-1/dqa62717/harmony-tests-d7xiPyK2v](https://app.snowflake.com/us-east-1/dqa62717/harmony-tests-d7xiPyK2v)
    * dbt test

#### The Expected Outputs from Your Contributions

1. Table that is consumable by the public with proper documentation.
2. Documentation that gets generated on [https://docs.harmony.metricsdao.xyz](https://docs.harmony.metricsdao.xyz).
3. Snowflake Marketplace data access.

#### Keys to Success

* Ask for help!
* Pair programming - ask in the Curator channel to partner with someone.
