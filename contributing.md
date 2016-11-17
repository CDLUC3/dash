---
layout: page
title: Contributing to Dash Development
permalink: /contributing/
---

_Note: you will need a GitHub account to contribute._

## Overview of Dash

Dash is an easy-to-use data preservation and publication service for the effective curation of and access to campus research data. It is designed to be a simple self-service curation tool for researchers to archive and share their datasets.

**Tasks Dash helps researchers perform:**

* Prepare data for curation by reviewing best practice guidance for the creation or acquisition of digital research data.
* Select data for curation through local file browse or drag-and-drop operation.
* Describe data in terms of the DataCite metadata schema.
* Identify data with a persistent DOI for permanent citation and discovery.
* Preserve, Manage, and Share data by uploading to a public Merritt collection.
* Discover and retrieve data through faceted search and browse.

### Code lines

There are multiple Dash repositories which make up the Stash framework providing the underlying code for the Dash service instance.

* **[dashv2](https://github.com/CDLUC3/dashv2)**: a Stash based Rails application
* **[stash_engine](https://github.com/CDLUC3/stash_engine)**: a Rails engine which houses code for the Store portion of Dash.  
* **[stash_datacite](https://github.com/CDLUC3/stash_datacite)**:  a Rails engine which houses the metadata schema supporting Datacite
* **[stash-sword](https://github.com/CDLUC3/stash-sword)**:: A minimal SWORD 2.0 connector providing those features needed for Stash.
* **[dash2-harvester](https://github.com/CDLUC3/dash2-harvester)**: It consists of a Ruby bundle and a wrapper script, bin/harvest.sh.

### Architecture
![Architecture](https://raw.githubusercontent.com/CDLUC3/dash/gh-pages/docs/stash_architecture.png)


## To contribute to the Stash frame and repositories, please contact us at uc3@ucop.edu

The Dash project will use the **Fork & Pull** model. This lets anyone fork an existing repository and push changes to their personal fork, without requiring access be granted to the source repository. The changes must then be pulled into the source repository by the project maintainer.

**Step 1. Fork the repository.** 

[Follow these steps from GitHub to fork a repository](https://help.github.com/articles/fork-a-repo)

**Step 2. Set up your Rails development environment.**


**Step 3. Make changes, additions, etc. to the code.**

Do this using your local development environment and dash-ingest forked repository.

**Step 4. Commit your changes and submit a pull request.**

Once you have committed and tested your code to your local repository, _complete with unit and integration tests_, you can notify the Dash project team via a pull request. [Instructions on this are available from GitHub](https://help.github.com/articles/using-pull-requests).

**Step 5. Changes merged (pending approval).**

After successful review of the pull request containing the proposed changes, the Dash project team will merge the pull request into the upstream repository (dash-ingest). [More information on merging a pull from GitHub](https://help.github.com/articles/merging-a-pull-request).

These changes will be deployed onto the CDL dash-dev.cdlib.org virtual machine.

### Setting up a test development server to test the entire Dash system
* [Apache configuration]({{ site.baseurl }}/infrastructure)
