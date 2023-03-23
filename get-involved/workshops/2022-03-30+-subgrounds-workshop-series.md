---
description: >-
  Join the subgrounds dev team in a three part series on using a Python library
  to query and build on the Graph!
---

# 2022-03-30+ Subgrounds Workshop Series

Subgrounds is a Python framework for interacting with the Graph and GraphQL APIs.&#x20;

{% embed url="https://discord.gg/YTaGq7eRbK" %}

{% embed url="https://github.com/Protean-Labs/subgrounds" %}

## When?

1. Wednesday, March 30th at 18:00 UTC / 2pm ET
2. Wednesday, April 6th at 18:00 UTC / 2pm ET
3. Wednesday, April 13th at 18:00 UTC / 2pm ET

## Series Outline

**The first part will be heavily focused on Subgrounds' core features and serve as a guide on how to start and complete data analytics using Subgrounds.**

Participants can expect the following topics to be covered:

* Intro: Motivations for Subgrounds and some GraphQL basics
* FieldPaths: What are they and how do we combine them to create subgrounds requests?
* `subgrounds.query` method: the simplest way to get data
* `subgrounds.query_df` method: get data in a flattened representation, returned in a pandas DataFrame
* `subgrounds.query_timeseries` method: query and return regularized timeseries data
  * Note: this is planned for the `v0.1.0` release and is not yet publicly available.
* Creating and using `SyntheticFields`&#x20;
* Querying non-Subgraph APIs with Subgrounds

**The second part would introduce building full featured analytics dashboards using Subgrounds built-in data visualization library called Dash. During this part, we will take a "live build" approach and create a simple klimaDAO analytics dashboard in this session. The dashboard will explore KlimaDAOs treasury and general protocol metrics.**

Expected topics:

* Introuction to dash and data visualizations with dash
* The Code: Preparing Subgrounds for your data exploration
* The Data: Interfacing Subgrounds with Dash
* App Layout section : Building and assembling your dashboard components and layout
* Callback: Connecting visualizations to Subgrounds queries
* Running your app locally
* Deploying your app to Heroku intro

**The third part would be a continuation of part two, except that rather than deploying locally to your machine, we will guide you on deploying to the cloud (Heroku), generating your unique URL, and sharing your dashboard as an app.**

Expected topics:

* Introduction to Heroku&#x20;
* Setting up Heroku account&#x20;
* Installing Heroku CLI&#x20;
* Creating App project folder on your IDE&#x20;
* Installing necessary App project libraries&#x20;
* Create necessary files for Heroku server&#x20;
* Deploy App to Heroku

## Recordings

### 2022-02-09 Community Call

The subgrounds team previously joined MetricsDAO on a community call to showcase their powerful library to the MetricsDAO commuity. The recording of that is available below and we recommend re-watching as a refresher or for any newcomer to both Subgrounds and the Graph.

{% embed url="https://www.youtube.com/watch?v=SklIyKNg22U" %}

{% file src="../../.gitbook/assets/Playgrounds x MetricsDAO.pdf" %}
Slide deck from the community call
{% endfile %}

### 2022-03-30 Part 1

{% embed url="https://youtu.be/osQft2dRm6A" %}

#### Re**sources**

{% file src="../../.gitbook/assets/Subgrounds Workshop #1 Under the Hood.pdf" %}

{% file src="../../.gitbook/assets/workshop.ipynb" %}
Follow along with this Jupyter notebook
{% endfile %}

### 2022-04-06 Part 2

{% embed url="https://youtu.be/zU2JGADVl_s" %}

#### Resources

{% embed url="https://github.com/Tachikoma000/Subgrounds_visualization_with_dash" %}

{% file src="../../.gitbook/assets/Subgrounds Workshop #2 Building Subgrounds Powered Apps.pdf" %}

{% embed url="https://dash.plotly.com/introduction" %}

{% embed url="https://dash-bootstrap-components.opensource.faculty.ai/docs/quickstart" %}
Dash Bootstrap
{% endembed %}

### 2022-04-13 Part 3

{% embed url="https://youtu.be/ye9JrDubRtI" %}

#### Resources

{% embed url="https://docs.google.com/document/d/1_VN5TsbsaLpthgh9OnyRgowM6Ahy6_tdxzgq5bNxtAY/edit?usp=sharing" %}
