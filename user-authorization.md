---
layout: page
title: User Authorization
permalink: /user-authorization/
---

### Note: This page refers to future work we _may_ undertake for the Dash tool. 

By default, the Dash application will allow any authenticated user to deposit content in the repository for their home campus. The home campus is determined by the Shibboleth Identity Provider (IdP) that validates the user's credentials. If someone is authenticated by the UCLA IdP, then they can deposit datasets in the UCLA instance of Dash. If they are authenticated by the Berkeley IdP, then they can deposit content in the Berkeley repository. Someone authenticated by the UCLA IdP cannot store content in any other campus repository. They can, however, search content at any campus.

**There may be a desire for finer-grained authorization.** For example, a campus might want to limit the ability to upload datasets to the campus instance of Dash to current faculty members only, or to faculty, researchers, and graduate students.

The roadmap for Dash includes plans to support finer-grained authorization. This does, however, require work on the part of the campus. 

## Enabling authorization for specific campus groups

A campus will be able to define an attribute, or set of attributes, that Dash can use to determine whether or not an authenticated individual is also authorized to add content to the campus Dash repository. These attributes must be delivered through the campus IdP upon authentication, as Shibboleth header variables. The process for doing this is straightforward. The Dash application already receives EPPN (a Shibboleth unique ID), email address, and a display name from the campus IdPs. If a campus wants to use finer-grained authorization, the process will look something like this:

1. Campus staff defines the authorization rules
1. Campus staff works with campus directory services and IdP to populate and release the necessary attributes to the Dash application
1. CDL staff configures the Dash application to request the necessary attributes from the IdP
1. Future version of the Dash application uses attributes to enforce authorization

The attributes can be used directly, or authorization can be determined by any arbitrary process and expressed as a single attribute. 

In the former case, for example, a campus might decide that if an individual is a member of any one of six groups in the campus LDAP directory, and they are in an academic position, they are authorized to use the campus Dash repository. The campus staff would work with the campus directory services and IdP managers to provide group membership and academic status to the campus IdP and release those attributes to the Dash application. A future version of the Dash application could then evaluate those attributes against the rules defined by the campus staff and make a decision about whether or not the authenticated user is also authorized.

If the authorization decision is complex or arbitrary, then the best solution is probably to create a new attribute in the campus directory service dedicated to Dash authorization. The campus staff can use any process at all to arrive at the authorization decision, and then assign a value of 'true' to the attribute, such as authorizedForDash=true. Again, the campus IdP must be configured obtain this new attribute from the directory and release it to Dash. A future version of the Dash application will then be able to use that attribute to grant or deny access to an authenticated user.
