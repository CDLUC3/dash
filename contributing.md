---
layout: page
title: Contributing to Dash Development
permalink: /contributing/
---

_Note: you will need a GitHub account to contribute._

## Overview of Dash

Dash is a new, easy-to-use solution for the effective curation of and access to campus research data. It is designed to be a simple self-service curation tool for researchers to archive and share their datasets.

**Tasks Dash helps researchers perform:**

* Prepare data for curation by reviewing best practice guidance for the creation or acquisition of digital research data.
* Select data for curation through local file browse or drag-and-drop operation.
* Describe data in terms of the DataCite metadata schema.
* Identify data with a persistent DOI for permanent citation and discovery.
* Preserve, Manage, and Share data by uploading to a public Merritt collection.
* Discover and retrieve data through faceted search and browse.

### Code lines

There are three Dash repositories which make up the DASH web application

* **[dash-ingest](https://github.com/CDLUC3/dash-ingest)**: houses code for the data ingest portion of Dash. Allows the user to create, describe and upload datasets, then submit them for deposit into Merritt.  Written in Ruby/Rails.
* **[dash-XTF](https://github.com/CDLUC3/dash-xtf)**: houses code for the discovery portion of Dash.  Allows the user to search and download datasets.  Written in [XTF](http://xtf.cdlib.org/).
* **[dash-harvester](https://github.com/CDLUC3/dash-harvester)**: A python script which parses an atom feed from Merritt for harvesting.

### Architecture
![Architecture](https://raw.githubusercontent.com/CDLUC3/dash/gh-pages/docs/DashArchitecture.png)


## To contribute to the dash-ingest repository

The Dash project will use the **Fork & Pull** model. This lets anyone fork an existing repository and push changes to their personal fork, without requiring access be granted to the source repository. The changes must then be pulled into the source repository by the project maintainer.

**Step 1. Fork the repository.** 

[Follow these steps from GitHub to fork the dash-ingest repository](https://help.github.com/articles/fork-a-repo)

**Step 2. Set up your Rails development environment.**

Information on setting up your Rails development environment locally can be found at [Operations: Rails development setup](https://cdluc3.github.io/dash/rails-setup)

**Step 3. Make changes, additions, etc. to the code.**

Do this using your local development environment and dash-ingest forked repository.

**Step 4. Commit your changes and submit a pull request.**

Once you have committed and tested your code to your local repository, _complete with unit and integration tests_, you can notify the Dash project team via a pull request. [Instructions on this are available from GitHub](https://help.github.com/articles/using-pull-requests).

**Step 5. Changes merged (pending approval).**

After successful review of the pull request containing the proposed changes, the Dash project team will merge the pull request into the upstream repository (dash-ingest). [More information on merging a pull from GitHub](https://help.github.com/articles/merging-a-pull-request).

These changes will be deployed onto the CDL dash-dev.cdlib.org virtual machine.

### Setting up a test development server to test the entire Dash system
* [Apache configuration](https://cdluc3.github.io/dash/infrastructure)
* [XTF Installation](https://cdluc3.github.io/dash/XTF-Installation) 
