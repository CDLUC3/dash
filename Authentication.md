---
layout: page
title: Operations: Authentication
permalink: /authentication/
---

## Current Scenario

Currently, the determination as to which Dash campus instance you land on is handled by **Apache**.  Apache detects any current sessions and if one is active, based on the session header information, directs the user to the proper dash campus instance.  If a session is not active, then the user selects their campus from the Discovery page and is routed to the proper IdP for authentication.  Once authenticated, Apache directs to the proper campus.

## What we need to support

For the DataUp authentication, users will authenticate using **GoogleID**.  After authentication the user will be directed to the dash.dataone.org instance. With GoogleID authentication, we are assuming that many (most?) campus users will also be authenticated to Google for Gmail, Drive, etc.  Therefore Apache cannot use the session header information and make the determination of where to route the user since they'll most likely be authenticated to Google and may want to go to a UC campus instance of Dash, not to the dataONE instance.  

## Solution

We need to ask the user which instance they would like and direct them to the proper authentication method. See flow chart below.

### If a Dash session exists

Redirect to the app - Requires Rails app to set something in Session Header.  Handled by Apache

### If no Dash session exists 

* check if Shib or Google ID session exists, 
  * No: prompt user to which site they want and direct to IdP  (can be handled by Apache?) 
  * Yes: check which session exist - ask user which Dash instance they want. Does the session match the site they want?  
    * No: Authenticate and then access Dash based on authentication.  Go to top of flow.
    * Yes: Create the DASH session (Rails) and access Dash (ingest)


**Flowchart on the left hand side (in blue) describes this:**
![](https://raw.githubusercontent.com/CDLUC3/dashdocs/master/authentication-flow-chart.jpg)

## Moving Authentication to Rails

**Problem**

* Asking the user which site that they want and if it matches is outside scope of Apache.  So it was suggested that this logic be all contained in the Rails application.  
* Rails would handle Shibboleth and GoogleID authentication via OmniAuth gem
* Have a login page where user selects UC campus or DataONE and then gets directed to proper IdP or ingest if already authenticated
* If we want to configure the shibboleth piece along with the UC authentication mechanisms, then the we need to make modifications to the Rails ingest to handle the discovery and selection page.

**Solution**

Proposal going forward is to set up 2nd VM to support Dash-DataUp application with Rails Omniauth authentication for Shibboleth & GoogleId

**Risks**

+ This requires changes to how apache directs requests to the rails piece.  
+ Will affect Berkeley release schedule by at least 2 weeks since we need to incorporate additional functionality into Rails application to support shibboleth and add logic to determine where user is going, design and implement Apache.
+ Possible changes to Shibboleth Incommon metadata to support 2nd VM.  Right now only set up for UCOP.  Rekha only has UCB credentials for testing.

Have 2nd Dash instance for DataUp testing only.   This will not affect the codeline for current Dash development Apache configuration which only supports the UC campuses.  UCI would also be able to contribute to the codeline.  

