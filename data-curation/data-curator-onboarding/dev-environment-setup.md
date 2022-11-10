---
description: A MetricsDAO guide to data curation development environment setup
---

# Dev Environment Setup

## Accepted Development Environments

As of October 2022, the Data Curation pod accepts the following as development environments: \*&#x20;

* dbt Cloud&#x20;
* dbt on Linux/MacOS&#x20;
* or dbt on Docker

All of these are just ways get a code development UI, be that the DBT Cloud IDE in the first case or VSCode in the latter two cases, to talk to dbt and then in turn getting dbt to talk to the MetricsDAO Snowflake data warehouse.

<figure><img src="../../.gitbook/assets/Data Curation Different Dev Envs.jpg" alt=""><figcaption></figcaption></figure>

_If you reached this document from the_ [_Data Curator Onboarding_](./) _page, you should have reached out to forg#9122 and/or issui#6571 on Discord in the_[ _General channel_](https://discord.com/channels/902943676685230100/903338987022876702) _or via DM to start the onboarding process. If not, do so by following the below steps to get Snowflake and Github access._

## Access

_Reach out to forg#9122 and/or issui#6571 on Discord in the_ [_General channel_](https://discord.com/channels/902943676685230100/903338987022876702) _or via DM to start this process._

### **Snowflake**

Hi, I’m interested in doing data curation for MetricsDAO, could you give me snowflake access_,_ please? I’d like my username to be: \[name]

Once you have been given the temporary password associated with your username, be sure to log in to the Snowflake UI at https://app.snowflake.com/us-east-1/dqa62717/ using your temporary password. Once you’re logged in, you should automatically be asked by Snowflake to change your temporary password to a real password of your choosing. If not, you can always go to your profile page to update your password.

![](https://lh4.googleusercontent.com/lEtuOjBkWTeQ6Ft2qAY7coYeHoNVYNYjA0d1zp6dbClHjwx9seZ1q\_AKIcYIbu4tjx4sY8ZSdefO3m-o3xyqYujK\_rwYy0dg88VovnsEueCmvOYdp5ZIxAzoDBlxLcfartgqlRVcKGb3zmj2ZYS7Cdenele8FliF4rslEi2tRkAEwCFZNtwJph5GwIpobg)



### **Github (optional)**

You have the option of asking to be added as a contributor to the MetrcsDAO repository. If this is the path you choose, send the following message to Forg or Issui:

* Hi, I’m interested in doing data curation for MetricsDAO, could you give me github access please? My github profile is: \[https://github.com/name]

However, the above step is optional because you don’t necessary need to be added to the MetricsDAO github repositories as a contributor in order to contribute changes to the code base. You can always follow the Fork and Pull Workflow by forking a copy of the MetricsDAO project to your github account. Just make sure to:

* Fork the MetricsDAO repository.
* Git clone from your forked repository. Ex: \`git clone [https://github.com/YourAccount/terra\_dbt](https://github.com/YourAccount/terra\_dbt)\`.
* Create a branch for the changes you'd like to make. Ex: \`git branch readme-update\`.
* Switch to the branch. Ex: `git checkout readme-update`.
* Make your changes on the branch and follow the rest of the steps in the [Fork and Pull Workflow ](https://reflectoring.io/github-fork-and-pull/\))to notify the MetricsDAO repository owners to review your changes.
* **Note:** In fact, the fork-and-pull workflow is the only workflow supported if you’re using dbt Cloud.

### **dbt Cloud**

The quickest way to start working is to use dbt Cloud. The Data Curation pod has put together a video to get you familiar with dbt concepts using dbt Cloud. However, if you’re already familiar with dbt and just want to quickly setup dbt Cloud with the MetricsDAO Snowflake, skip to 49:25 of [the video](https://youtu.be/Cw41rjFjraQ).

* dbt Cloud basics & Snowflake [5:20](https://www.youtube.com/watch?v=Cw41rjFjraQ\&t=320s)
* dbt best practices [28:20](https://www.youtube.com/watch?v=Cw41rjFjraQ\&t=1700s)
* dbt testing and documentation[ 41:09](https://www.youtube.com/watch?v=Cw41rjFjraQ\&t=2469s)
* using dbt Cloud with a real MetricsDAO project[ 49:25](https://www.youtube.com/watch?v=Cw41rjFjraQ\&t=2965s)

### dbt on Docker

* Install Git (if you don’t have it): [https://git-scm.com/book/en/v2/Getting-Started-Installing-Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* Get Docker ( [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/) )
* Follow Docker setup
  * [https://github.com/MetricsDAO/harmony\_dbt#readme](https://github.com/MetricsDAO/harmony\_dbt#readme)
* Install [VSCode](https://code.visualstudio.com/)

For Windows users, you'll need to install WSL and connect VSCode to WSL by

* Right-clicking VSCode and running VSCode as admin.&#x20;
* Installing WSL by typing `wsl --install` in VScode's terminal.
* Following the rest of the VSCode WSL instructions to create a new WSL user.
* Installing the Remote Development extension (ms-vscode-remote.vscode-remote-extensionpack) in VSCode.
* Finally, restarting VSCode in a directory in which you'd like to work. For example,Finally, restarting VSCode in a directory in which you'd like to work. For example,
  * \`cd \~/metricsDAO/data\_curation/terra\_dbt\`
  * \`code .\`
  * [https://github.com/MetricsDAO/terra\_dbt#readme​](https://github.com/MetricsDAO/terra\_dbt#readme%E2%80%8B)
* Clone the project or MetricsDao Github repo `git clone https://github.com/MetricsDAO/harmony_dbt`
* Copy `.env.sample` and create `.env`, replace the highlights below with your own account and passwords
* ![](<../../.gitbook/assets/image (12) (1) (2).png>)
*   Install the dbt formatter from VS Code. For ease of use, turn on "format on save" by searching for "format" in the settings menu.

    * henriblancke.vscode-dbt-formatter


* Assume you have completed all of the steps above successfully, you’re ready to start the dbt console where you can make and test your models.
  * In VSCode’s terminal, type `cd <your dbt project>`. Ex: `cd terra_dbt`.
  * Then run \`make dbt-console\`
  * You can verify that the above command ran successfully by looking at the terminal prompt. It should have changed from your Linux bash promp to something like root@3527b394aaf0://terra#. Alternatively, you can see in the Docker Desktop app that an instance of the terra\_dbt is now running.

### dbt on Linux or MacOS

We are still in the process of documenting the procedure for direct dbt installation on Linux or MacOS. More to following before the end of 2022.

* (Optional) Install dbt on your terminal:[ https://docs.getdbt.com/dbt-cli/install/overview](https://docs.getdbt.com/dbt-cli/install/overview)**​**

#### Channels

Drop your questions in the Curator’s Channel (Let's open it up to the public / People can leave feedback relating to the data in the snowflake database.)

#### Simple Walkthrough of How to Contribute

This is going to be a very rough guide on what is expected. You can consider it as a living document that will get updated again and again.

#### Workshop on Data Curation and dbt

chuxin.eth ran a workshop in March 2022 on using dbt to curate tables. Feel free to follow-up with any questions from this in Discord!

{% embed url="https://youtu.be/wj_2ljFABuA" %}
Data Curation with Chuxin
{% endembed %}

#### The dbt style guide and model standardsl we follow

{% embed url="https://github.com/dbt-labs/corp/blob/master/dbt_style_guide.md" %}
https://github.com/dbt-labs/corp/blob/master/dbt\_style\_guide.md
{% endembed %}

{% content-ref url="../../get-involved/data-curation/data-modeling-standards.md" %}
[data-modeling-standards.md](../../get-involved/data-curation/data-modeling-standards.md)
{% endcontent-ref %}

#### Steps to start contributing:

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

#### Current Season Pod Leaders&#x20;

* forg#9122 (Jack)
* issui#6571 (Issui)

### MetricsDAO Created Tables

#### Harmony Transactions

https://docs.harmony.metricsdao.xyz/#!/model/model.harmony.txs

#### Existing resources

* https://metricsdao.gitbook.io/internal-wiki/project-teams/analytics-stack
* https://www.getdbt.com/docs/
* https://rogerdudler.github.io/git-guide/

## FAQ

* C:\Users\ant>make 'make' is not recognized as an internal or external command, operable program or batch file. Install make for windows @ http://gnuwin32.sourceforge.net/packages/make.htm
* Something doesn’t work on the docker container. Try git clean -xdf to clean up the whole repo. Your .env file will be removed and thus please remember to save your password.
* What Python version can I use? As of v1.0.0, dbt-core is compatible with Python versions 3.7, 3.8, and 3.9.
