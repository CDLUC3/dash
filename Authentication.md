---
layout: page
title: Authentication
permalink: /authentication/
---

## OmniAuth

Authentication is supported by both  InCommon/Shibboleth institutional (SAML protocol) or OAuth2 social credentials.  These strategies are supported with the omniauth gems omniauth-shibboleth and omniauth-google-oauth2.

OmniAuth Shibboleth strategy uses the 'auth hash' for providing user attributes passed by a Shibboleth Service Provider (SP). It enables developers to use Shibboleth and the other authentication methods, including local auth, together in one application.  The DASH application uses a slight variant of the [omniauth-shibboleth gem](https://bitbucket.org/cdl/omniauth-shibboleth) to work with headers as opposed to environment variables.

omniauth-google-oauth2 strategy also uses the auth hash as defined in the [gem](https://github.com/zquestz/omniauth-google-oauth2).

For the Dash application, authentication is invoked when a user would like to manage or create datasets for submission.  This is done by selecting My Datasets from the top menu bar.  For ONEShare users, users visiting oneshare.cdlib.org, are authenticated via Google credentials while UC campuses are authenticated via their campus via Shibboleth credentials.  
If the user is already authenticated (i.e. logged in), they will be presented with a table of their current datasets.

If they are not authenticated, the workflow for determining their authentication is as follows.

![Dash Authentication Workflow]({{ site.baseurl }}/images/dash_authentication.png)



