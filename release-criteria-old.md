---
layout: page
title: Dash Production Release Criteria (older version)
permalink: /release-criteria-old/
---

### _This is a previous version of the [current DataONE Dash Release Criteria document](http://cdluc3.github.io/dash/release-criteria/)_

The following features should be tested, documented, and available as a precondition to the production release (V1) of Dash.

### Infrastructure

* Three parallel Dash VM instances (dash-dev.cdlib.org, dash-stage.cdlib.org, dash.cdlib.org), each configured with the full technology stack:
  * Apache 2.4.<u>x</u> SSL-enabled, reverse proxy web server
  * Ruby 2.<u>x</u>
  * Rails 3.<u>x</u> application framework
  * Unicorn 4.<u>x</u> web server
  * XTF 3.1
  * Tomcat
  * J2SE 1.5.0 or newer
  * Python 2.7.6 for metadata harvester
  * Server certificates
  * Start-up scripts (init.d)
* Codebase managed in GitHub repositories, one each for ingest, harvest, and XTF, but all under the umbrella of a common UC3 dash administrative user.
* Deployment scripts for infrastructure (puppet).
* Deployment scripts for application.

### Policies

* Standardized submission agreement
* Standardized data use agreement (DUA)
  * Do we want to make Merritt display of formatted DUAs a pre-condition?  (Assuming that the final DUA terms will be much simpler and shorter than the UCSF prototype, perhaps this isn’t a problem.)
* (Per campus?) Maximum size of individual dataset files and datasets
* Maximum size of individual campus collections
* Outline of eventual price model and identification of which campus units will be financially responsible.  (We’ll probably go live before we get final UCOP approval; all data extant at the time of approval will be exempt from pricing calculations.)

### Application features

* Branding
  * Direct access to campus-specific URLs (e.g., dash.berkeley.edu) or campus selection page from the generic URL (dash.cdlib.org).
  * Campus-specific logo in all headers (ingest and XTF).
  * Campus-specific “Contact us”, to be mailed to campus-designated email address (and to a UC3 email), in all footers.
  * Campus-specific attribution in all footers, e.g., “Dash is a collaborative project of the UC <campus> Library and UC3”.
  * Campus-specific text for About and FAQ pages.
* Contribution/Submission
  * Shibboleth-based authentication.
  * File browse and drag-and-drop dataset selection, subject to maximum dataset and file size limits.
  * Metadata entry form, with tooltip for each element:
    * Title
    * “Data type” (dropdown of the DataCite types and “Presentation” and “Poster”)
    * Creator and optional ANDS ORCID widget (repeatable)
    * Keywords (repeatable)
    * Abstract
    * Methods
    * Citations (repeatable)
  * “Institution” will be automatically defined based on the campus implied by their Shibboleth authentication attributes.
  * Opportunity to review metadata and add/delete files prior to submission.
  * Automated packaging and submission to the Merritt ONEShare collection.
* Discovery: Faceted XTF search and browse, with faceting of all DataCite metadata elements.
* Miscellaneous
  * Pages for “About”, “Terms of service”, “FAQ”, “Policies” in all footers.
  * “Contact Us” page

### Configuration

* Virtual hosts and other Shibboleth integration for the two early adopter campuses: UCB and UCLA; easy enhancement path for other campuses desiring participation.
* Merritt Dash user role accounts (one per campus with submission privileges). 
* Public Merritt collections for UCB and UCLA.
* Submission profiles for UCB and UCLA collections, using the VM-based storage service (uc3-mrt-store.cdlib.org) to deposit data in the SDSC (primary) and UCLA (secondary) storage nodes with assigned DOIs.
* EZID DOI minter for UCB and UCLA.
* Maximum size of individual campus collections.

### Operations

* Cron job for Python harvesting script.
* Groundwork/Nagios monitors.
* Weekly report of the total and incremental number and size of datasets by campus/Merritt collection, mailed to designated campus contacts.


