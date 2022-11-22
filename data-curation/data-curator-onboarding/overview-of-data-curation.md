---
description: A high level overview of data curation at MetricsDAO.
---

# Overview of Data Curation

Data curation is the process of creating the data tables that power MetricsDAO bounties and analyses.

This page gives a high level overview of data curation and describes how curation projects are organized and coordinated at MetricsDAO.

Want to get involved? Read the [Data Curator Onboarding page](https://docs.metricsdao.xyz/data-curation/data-curator-onboarding).

## A High Level Overview of Data Curation <a href="#docs-internal-guid-e935f75a-7fff-4f64-b3db-665166109a0c" id="docs-internal-guid-e935f75a-7fff-4f64-b3db-665166109a0c"></a>

At a high level, data curators write SQL code to transform blockchain data into easy to use formats.

For example, a curator will write SQL to transform JSON bytecode data into a table that is human readable, organized, and easy to query. Or a curator will write SQL to combine data from existing tables into a new table for a specific protocol or specialized analysis.

Each step in the data curation process involves transforming data into progressively easier to use formats.

To better understand these steps it helps to see them in the context of the full blockchain data journey: starting with a person using a dApp and ending with analysts creating insights from curated data tables:

| Step in the Blockchain Data Journey                                                                                                                                 | Data Format                                                                                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <ul><li>A person transacts with a dApp, or a contract transacts with another contract.</li></ul>                                                                    | <ul><li>Data for these events are stored in the chain’s native binary format for computation and inclusion in a block.</li></ul>                                                                                                         |
| <ul><li>The chain logs these events and includes them them in a block with thousands of other events.</li></ul>                                                     | <ul><li>Data remain in the chain’s native binary format e.g. EVM bytecode.</li></ul>                                                                                                                                                     |
| <ul><li>A MetricsDAO data provider partner pulls blocks from a node provider into MetricsDAO’s Snowflake database.</li></ul>                                        | <ul><li>Data are now stored in a few basic tables (e.g. blocks &#x26; transactions) in raw format. Data fields are a mix of values, arrays, and JSON objects containing both hexadecimal bytecode and decoded readable values.</li></ul> |
| <ul><li><strong>Data curators</strong> model the raw blocks data into core tables.</li></ul>                                                                        | <ul><li>All remaining data in bytecode are decoded into readable format and data are transformed and organized into core tables that adhere to strict data modeling standards.</li></ul>                                                 |
| <ul><li><strong>Data curators</strong> create additional tables from the core tables, testing and refining them until they're ready for public analytics.</li></ul> | <ul><li>Data in core tables are transformed and combined as needed into easy tables for public release.</li></ul>                                                                                                                        |
| <ul><li>Analysts use SQL to query the final tables to uncover insights and solve analytics bounties.</li></ul>                                                      | <ul><li>Data are ‘transformed’ into results, insights, and visualizations.</li></ul>                                                                                                                                                     |

With each transformation curators need to deeply understand the data they’re modeling. They’ll make design decisions, write tests, write documentation, incorporate user feedback, and more during the phases of a curation project.

## Project Phases <a href="#docs-internal-guid-e0f771e4-7fff-a462-debd-ccbecf41b7e5" id="docs-internal-guid-e0f771e4-7fff-a462-debd-ccbecf41b7e5"></a>

### Curating a Protocol or Specialty Table <a href="#docs-internal-guid-e0f771e4-7fff-a462-debd-ccbecf41b7e5" id="docs-internal-guid-e0f771e4-7fff-a462-debd-ccbecf41b7e5"></a>

Curation projects that create tables for a protocol like a DEX generally follow these phases:

#### Phase 1: Understand the protocol & its on-chain data

Deep dive to understand the protocol: from the perspective of its users (try it out!), and from the perspective of its founders and builders: what are their analytical needs and ecosystem priorities?\
\
If the curation team is building a specialty table for a chain, such as NFT sales, then they’ll work to anticipate analytical needs for that table.

With their understanding of the protocol, they’ll perform test transactions and examine how the protocol’s data show up in the core tables of its base layer chain(s).

#### Phase 2: Design & model the table(s)

The curation team will design and model the tables, working from the data in the protocol’s base layer chain(s).

#### Phase 3: Initial testing

The team writes tests on the new tables and releases them to users for querying and feedback.

#### Phase 4: Final testing, bug resolution, and release

Final tests written and resolution of any bugs. Release tables to public.

#### Phase 5: Continuous iteration and improvement

Work with the community to prioritize improvements and new tables based on feedback and the protocol’s needs evolve.



### Curating an Entire Chain

Curation projects that create tables for an entire chain like Near or Terra are broken down into phases:

#### Phase 1: Ingest data from a node

One of MetricsDAO’s data providers, like Flipside, will ingest data from a node provider and into MetricsDAO’s Snowflake database.

#### Phase 2: Design & model core schemas

The curation team will design and model tables like blocks, transactions, and messages.

#### Phase 3: Initial testing

The curation team writes tests on core tables and releases the core tables to users who use the tables and provide feedback.

#### Phase 4: Model the data into tables ready for analytics

The curation team models the data into core tables into final tables ready for analytics.

#### Phase 5: Testing and bug resolution

Final tests written and resolution of any bugs.

#### Phase 6: Continuous iteration and improvement

Work with the community to prioritize improvements and new tables based on feedback and as new protocols/projects launch on the chain.\


To see an example of these phases with more details check out [this Notion page for the Terra 2.0 curation project planning](https://www.notion.so/Terra-2-0-Data-Curation-Planning-930fcefd2c79439591e977b3e42ce288).

After an entire chain’s data has been curated, new projects may launch that focus on creating tables for a specific protocol or project like Uniswap.  New projects may also launch to create  specific tables like NFT mints and sales.

## Project Roles <a href="#docs-internal-guid-aace5803-7fff-7008-e0b6-3385de5a9734" id="docs-internal-guid-aace5803-7fff-7008-e0b6-3385de5a9734"></a>

See the [Data Curator Onboarding page](./) for more details on curator roles and how to get involved.

## Project Tools & Coordination <a href="#docs-internal-guid-4fdbe059-7fff-a63c-ab45-18b7c55a54f2" id="docs-internal-guid-4fdbe059-7fff-a63c-ab45-18b7c55a54f2"></a>

In addition to the [developer tools](dev-environment-setup.md) that curators use to write code, curators will coordinate project work via:

* Coordinape for group consensus on contributor compensation.
* Github Projects, a section of our [Github](https://github.com/MetricsDAO/) that organizes work by assignee, issues and pull requests.
* Notion (again see the [Terra 2.0 planning](https://www.notion.so/Terra-2-0-Data-Curation-Planning-930fcefd2c79439591e977b3e42ce288) example).
* [Discord](https://discord.gg/p3GMjK2zAr) including a curators channel and weekly voice channel meetings.

## Get Started & Learn from the Curator Community

This page describes how curation projects are organized and coordinated, but in practice we learn the most from each other. The most important details will come from participating, shadowing, and learning from the MetricsDAO community. See the [Data Curator Onboarding page](./) to get started.
