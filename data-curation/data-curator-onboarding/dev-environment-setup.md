---
description: A MetricsDAO guide to setting up your data curation development environment.
---

# Dev Environment Setup

MetricsDAO curators use three primary tools**:**

| Tool                                                                | Used for                                                      |
| ------------------------------------------------------------------- | ------------------------------------------------------------- |
| [Snowflake](dev-environment-setup.md#snowflake-access-and-setup)    | Querying tables & connecting to third party tools             |
| [Github](dev-environment-setup.md#github-optional)                  | Viewing technical documentation, contributing & collaboration |
| [dbt Access & Setup](dev-environment-setup.md#dbt-access-and-setup) | Curating table designs                                        |

See below for details on setup and access for each tool.



## **Snowflake Access & Setup**

Once you have been given the temporary password associated with your username, be sure to log in to the Snowflake UI at https://app.snowflake.com/us-east-1/dqa62717/ using your temporary password. Once you’re logged in, you should automatically be asked by Snowflake to change your temporary password to a real password of your choosing. If not, you can always go to your profile page to update your password.

![](https://lh4.googleusercontent.com/lEtuOjBkWTeQ6Ft2qAY7coYeHoNVYNYjA0d1zp6dbClHjwx9seZ1q\_AKIcYIbu4tjx4sY8ZSdefO3m-o3xyqYujK\_rwYy0dg88VovnsEueCmvOYdp5ZIxAzoDBlxLcfartgqlRVcKGb3zmj2ZYS7Cdenele8FliF4rslEi2tRkAEwCFZNtwJph5GwIpobg)



## **Github Access & Workflow**

You have two options to contribute to MetricsDAO's Github repository:

* Option 1: Follow the Fork and Pull Workflow with your own Github (see below)
* Option 2: Be added as a contributor to the [MetricsDAO Github](https://github.com/MetricsDAO) and commit directly to project repositories with pull requests

The Fork and Pull Workflow is:

* Fork the MetricsDAO repository to your Github.
* Git clone from your forked repository to your local machine. ex: `git clone` [`https://github.com/YourAccount/terra_dbt`](https://github.com/YourAccount/terra\_dbt)\`
* Create a branch for the changes you'd like to make. Example: `git branch readme-update`.
* Switch to the branch. Ex: `git checkout readme-update`.
* Make your changes on the branch and follow the rest of the steps in the [Fork and Pull Workflow ](https://reflectoring.io/github-fork-and-pull/\))to notify the MetricsDAO repository owners to review your changes.
* **Note:** In fact, the fork-and-pull workflow is the only workflow supported if you’re using dbt Cloud for your dbt development environment (more on dbt below).

## dbt Access & Setup

### Accepted dbt Development Environments <a href="#accepted-development-environments" id="accepted-development-environments"></a>

As of October 2022, the Data Curation pod accepts the following as development environments:&#x20;

* dbt Cloud
* dbt on Linux/MacOS&#x20;
* dbt on Docker on Linux/MacOS (or Windows with [WSL](dev-environment-setup.md#windows-wsl))

All of these are just ways get a code development UI, be that the DBT Cloud IDE in the first case or VSCode in the latter two cases, to talk to dbt and then in turn getting dbt to talk to the MetricsDAO Snowflake data warehouse.

<figure><img src="../../.gitbook/assets/Data Curation Different Dev Envs.jpg" alt=""><figcaption></figcaption></figure>

### **dbt Cloud**

The quickest way to start working is to use dbt Cloud. The Data Curation pod has put together a video to get you familiar with dbt concepts using dbt Cloud. However, if you’re already familiar with dbt and just want to quickly setup dbt Cloud with the MetricsDAO Snowflake, skip to 49:25 of [the video](https://youtu.be/OarXSXOjL0c).

* dbt Cloud basics & Snowflake [5:10](https://youtu.be/OarXSXOjL0c?t=310)
* dbt best practices [28:20](https://youtu.be/OarXSXOjL0c?t=1700)
* dbt testing and documentation [41:09](https://youtu.be/OarXSXOjL0c?t=2470)
* using dbt Cloud with a real MetricsDAO project [49:30](https://youtu.be/OarXSXOjL0c?t=2969)

### dbt via the Command Line

dbt is available for installation via several popular package managers, including Homebrew and pip.

Follow the instructions on dbt Labs' documentation to get dbt set-up on your machine:

{% embed url="https://docs.getdbt.com/docs/get-started/installation" %}

### dbt on Docker

To manage dependencies and account for differences in machines, Docker may be used to create a dbt terminal for development.

* Install Git (if you don’t have it): [https://git-scm.com/book/en/v2/Getting-Started-Installing-Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* Get Docker ( [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/) )
* Follow Docker setup
  * [https://github.com/MetricsDAO/harmony\_dbt#readme](https://github.com/MetricsDAO/harmony\_dbt#readme)
* Install [VSCode](https://code.visualstudio.com/)

#### dbt on Docker with Windows WSL

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

## FAQ

* C:\Users\xyz>make 'make' is not recognized as an internal or external command, operable program or batch file.&#x20;
  * Install make for windows @ http://gnuwin32.sourceforge.net/packages/make.htm
* Something doesn’t work on the docker container.&#x20;
  * Try git clean -xdf to clean up the whole repo.&#x20;
  * Your .env file will be removed and thus please remember to save your password.
* What Python version can I use?&#x20;
  * As of v1.0.0, dbt-core is compatible with Python versions 3.7, 3.8, and 3.9.
