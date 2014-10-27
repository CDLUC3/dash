---
layout: page
title: Infrastructure
permalink: /infrastructure/
---

## Overview

Dash is a UC-specific iteration of the Datashare application. It was renamed to avoid confusion with several other initiatives with the same name. The design goal for the infrastructure is to provide a campus-specific URL for each UC campus, but run only one instance of the application behind the scenes. To accomplish this, it was necessary to configure DNS, Shibboleth, and a series of Apache virtual hosts. Dash runs on a single VM, with one instance in development, one in staging, and one in production.

## Development Environment

The Dash development environment runs on the virtual machine uc3-datashare-dev.cdlib.org. This is a Novell SLES VM.

### DNS Configuration:

Each campus that participates in Dash must register a DNS name of 'dash-dev.[campus TLD]' or 'dev.dash.[campus TLD]. Examples are dash-dev.berkeley.edu or dev.dash.ucla.edu. This DNS name must resolve to uc3-datashare-dev.cdlib.org.

### Apache Configuration:

There is a standard httpd.conf file that sets very few parameters for the Apache server. That file has an Include statement to read in vhost-base.conf. The vhost-base.conf file defines the overall global behavior of the server. It redirects all http requests to https, for security, for each virtual host. The vhost-base.conf file then has an Include statement to read in a vhost configuration for each participating campus.

An overall brochure site is available at http://dash-dev.cdlib.org. This is largely a static site. It provides general information about the Dash application, and allows the user to select their institution. Upon selecting an institution, the user is routed to the virtual host for their particular instance of Dash.

For each participating campus, there is an Apache virtual host defined to respond to the URL for that campus. For example, a request made to http://dash-dev.berkeley.edu is sent to the dash-dev.berkeley.edu virtual host. The vhost configuration for each campus defines a campus-specific document root, a campus-specific certificate and key for SSL, campus-specific log files, basic Shibboleth configuration, and rewrite rules to route requests to the backend XTF and Ruby applications at ports 8085 and 8080, respectively. Ports 8085 and 8080 are locked down by local firewall rules so they will only accept connections from the localhost or specific campus reverse proxy servers. This forces all connections to go through an Apache proxy. An example configuration file is attached to this Wiki page, at the top.

The document root directories are used to deliver static content that gives each virtual host a campus-specific identity. Elements such as campus logos and boilerplate text are kept here. Campus-specific certificates are used to prevent users from seeing security exceptions in their browser when they access the application via SSL.

Instances of Dash are running at http://dash-dev.ucop.edu, dash-stg.ucop.edu, and dash.ucop.edu, to accommodate CDL needs.

### Shibboleth Configuration:

A  Shibboleth Service Provider is embedded within the Rails Dash Ingest application running at port 8085. The entity ID is "https://dash.cdlib.org/shibboleth". The associated SP metadata has endpoints configured to route responses to the correct Apache virtual host for each campus, in the development, staging, and production environments. These are the key elements to define a campus endpoint:

DiscoveryResponse element: Each campus must have a DiscoveryResponse element defined, to route Shibboleth authentication requests to the Shibboleth SP with the correct DNS name embedded in the redirect. Here is the one for UC Berkeley's development instance:

```` 
    <DiscoveryResponse xmlns="urn:oasis:names:tc:SAML:profiles:SSO:idp-discovery-protocol" Binding="urn:oasis:names:tc:SAML:profiles:SSO:idp-discovery-protocol" Location="https://dash-dev.berkeley.edu/Shibboleth.sso/Login" index="3"/>
````

AssertionConsumerService elements: Each campus must have AssertionConsumerService elements defined, to receive the assertions of identity from the campus Identity Providers. Typically, there will be four AssertionConsumerService elements, for SAML 1.0 POST, SAML 1.0 Artifact, SAML 2.0 POST, and SAML 2.0 Artifact. Here is a typical AssertionConsumerService element -

````
    <md:AssertionConsumerService xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata" index="9" Binding="urn:oasis:names:tc:SAML:1.0:profiles:browser-post" Location="https://dash-dev.berkeley.edu/Shibboleth.sso/SAML/POST"/>
````

Rather than define a specific set of attributes for the Dash application and doing a one-by-one integration with each campus IDP, the Dash application is registered with UCTrust (http://www.ucop.edu/information-technology-services//initiatives/uctrust-the-university-of-california-identity.html) ﻿(work in progress as of 4/2014). As part of the UCTrust initiative, every campus IDP will automatically recognize the Dash SP and release a standard set of attributes. Dash is also registered with InCommon as part of the Research and Scholarship category (https://spaces.internet2.edu/display/InCFederation/Research+and+Scholarship+Category). This is similar to UCTrust, in that it means that any Identity Provider that recognizes the Research and Scholarship category will automatically release a standard set of requested attributes to the Dash SP.

Dash uses a local discovery service that is part of the Rails Dash Ingest application. Please see the documentation for Dash Ingest (https://github.com/CDLUC3/dash-ingest) for more information.

## Staging Environment

The staging environment is essentially identical to development, but it is implemented on uc3-dash-stg.cdlib.org, and the various URLs, endpoints, and DNS names use 'stg' instead of dev, e.g. dash-stg.berkeley.edu or stg.dash.ucla.edu.

## Production Environment
The production environment is essentially identical to development and staging, but it is implemented on cdl-dash-p01.ucop.edu, and the various URLs, endpoints, and DNS names have no qualifier, e.g. dash.berkeley.edu or dash.ucla.edu.
