---
layout: page
title: Rights, Ownership, and Licenses
permalink: /Rights-Ownership-Licenses/
---

Information about rights, ownership and licenses for datasets

## Ownership of research data
The Academic Personnel Policy (APM) 020 states:
>Notebooks and other original records of the research are the property of the University.” (II. 5, p.3)

which the university interprets as meaning that research data are owned by the university. UCOP General Counsel currently recommends a CC-BY 4.0 license, requiring attribution, but they continue to study the issue. We should design Dash to be flexible in both accepting and displaying metadata for datasets with differing licenses.

There are several places in Dash where this matters:

* The ingest module, where the researcher fills in the metadata
* The XTF module, where the metadata are displayed
* The various static pages on policies, FAQs and help.

## Dash metadata
The DataCite schema v3 includes an element for rights. We currently do not use it, but we should include the rights information for each dataset in this metadata element. The DataCite metadata are distributed through Datacite to the Data Citation Index and other third parties, separate from the datasets, and should carry rights information.

While UCOP recommends using CC-BY, we already have a dataset with a CC0 license (doi:10.5068/D1WC7K), and we also know that the UCSF DataShare data have a custom data use agreement.

## Changes to Dash Ingest (Rails)
1. Add a rights table to the database. This would consist of  three fields: ID, Rights URI (varchar) and Rights Statement (varchar). Since the text accompanying the license will not be editable, there is no need to store in each dataset record.
1. Add a rights_id field to the records table. This would point to the id of the rights statement associated with the dataset.
1. Add a rights text field to the metadata input screen. It would not be editable, and would contain the text “CC-BY 4.0”. If this option changes or expands later to include other options, we could make this a dropdown or radio button list.
1. Add a “tool-tip” for this field with more information about CC-BY 4.0, and a link to a page explicitly about rights (see item IV.1 below).
1. Remove the rights checkbox from /app/views/records/review.html.erb
1. Add the rights XML field to the output of /apps/models/record.rb that is submitted to Merritt as mrt-datacite.xml. It should look something like this:

```` 
<rightsList>
<rights rightsURI=” https://creativecommons.org/licenses/by/4.0/”>[Approved wording for CC-BY submissions]</rights>
</rightsList>
````

## Changes to Dash XTF
1. Add a static page about rights. Currently, most static pages are in XTF. We plan to move static pages to Rails, but I’m not sure of the schedule.
1. Update these pages with information on Rights:
  * https://dash-dev.ucop.edu/xtf/search?smode=metadataBasicsPage
  * https://dash-dev.ucop.edu/xtf/search?smode=faqPage (campus-specific info)
  * https://dash-dev.ucop.edu/xtf/search?smode=uploadFaqPage
  * https://dash-dev.ucop.edu/xtf/search?smode=policiesPage
1. Change the item-level display to parse and display rights information from mrt-datacite.xml. E.g.:

    ````
        https://dash-dev.ucop.edu/xtf/view?docId=ucb/ark%2B%3D99999%3Dfk4893jsd/mrt-datacite.xml;query= 
    ````

4. This stylesheet (lines 304-306) currently hard-codes the license: 

    ````
        /xtf/style/dynaXML/docFormatter/default/docFormatter.xsl 
    ````

  * This needs to be changed to
  * Display the text and links in mrt-datacite.xml
  * Display the appropriate logo. The CC0 and CC-BY logos should be copied and stored locally.
  * Have a default display for mrt-datacite.xml files without rights information.