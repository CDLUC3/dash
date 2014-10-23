---
layout: page
title: Dash Production Release Criteria
permalink: /release-criteria/
---

The following features should be tested, documented, and available as a precondition to the production release of DataONE Dash.

### Infrastructure

* DataONE support in all three parallel Dash VM instances (dash-dev.cdlib.org, dash-stage.cdlib.org, dash.cdlib.org), each configured with the full technology stack:
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
* Deployment scripts for application and brochure pages (capistrano).

### Policies

Standardized submission agreement & data use agreement (CC-0)

* Maximum size of individual dataset files and datasets
* Maximum size of individual campus collections
* No price model necessary since storage paid for by UNM

### Application features

* Branding
  * URL: oneshare.cdlib.org
  * DataONE logo in all headers (ingest and XTF).
  * “Contact us” in all footers goes to UC3 email only (not DataONE)
  * Attribution in all footers, e.g., “DataONE Dash is a collaborative project of the DataONE project, University of New Mexico, and UC3”.
  * DataONE-specific text for About and FAQ pages.
* Contribution/Submission
  * OAuth-based authentication with Google credentials, supported in the Ruby/Rails application using the OmniAuth gem.
  * File browse and drag-and-drop dataset selection, subject to maximum dataset and file size limits.
  * Metadata entry form, with tooltip for each element:
    * Title
    * Data type - pick list
    * Author (repeatable)
    * Keywords (3 required + repeatable)
    * Abstract
    * Methods
    * Link (repeatable): identifier + identifier type (pick list) + description (pick list)
    * Identifier
    * Funder
    * Grant number
  * Auto-filled fields in metadata:
    * Date - YYYY
    * Institution - ONEShare
    * Rights - CC-0 
    * Rights URI - http://creativecommons.org/publicdomain/zero/1.0/
    * Opportunity to review metadata and add/delete files prior to submission.
  * Automated packaging and submission to the Merritt ONEShare collection.
    * Creation of equivalent DataCite and Dublin Core metadata files, see the crosswalk
    * Creation of the DataONE manifest file. There will be a pair of lines (one for “mrt-datacite.xml” and one for “mrt-dc.xml”) for each data <u>file</u> in the submission.
            <code>#%dataonem_0.1
            #%profile | http://uc3.cdlib.org/registry/ingest/manifest/mrt-dataone-manifest
            #%prefix | dom: | http://uc3.cdlib.org/ontology/dataonem#
            #%prefix | mrt: | http://uc3.cdlib.org/ontology/mom#
            #%fields | dom:scienceMetadataFile | dom:scienceMetadataFormat | dom:scienceDataFile | mrt:mimeType
            mrt-datacite.xml | http://schema.datacite.org/meta/kernel-3/metadata.xsd | <u>file</u> | text/xml
            mrt-dc.txt | http://dublincore.org/schemas/xmls/qdc/2008/02/11/qualifieddc.xsd | <u>file</u> | text/xml
            ...
            #%eof</code>
* Discovery: Faceted XTF search and browse, with faceting of all DataCite metadata elements.
* Miscellaneous
  * Pages for “About”, “Terms of service”, “FAQ”, “Policies” in all footers.
  * “Contact Us” page
* Configuration
  * OAuth-based authentication with Google credentials, supported in the Ruby/Rails application with the OmniAuth gem.
  * Merritt ONEShare user role account. 
  * Public Merritt ONEShare collection (already existing).
  * Submission profile for the ONEShare collection, using the VM-based storage service (uc3-mrt-store.cdlib.org) to deposit data in the UNM storage node with assigned DOIs and register with the Merritt member node.  [Work with Mark to modify the existing DataUp profile]
  * EZID DOI minter for ONEShare.  DataONE will become an EZID member.
  * Maximum size of individual campus collections.
* Operations
  * Cron job for Python harvesting script.
  * Groundwork/Nagios monitors.
  * Weekly report of the total and incremental number and size of datasets by campus/Merritt collection, mailed to designated campus contacts.


