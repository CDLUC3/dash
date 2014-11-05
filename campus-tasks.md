---
layout: page
title: Campus Tasks
permalink: /campus-tasks/
---

## Certificates
1. Decide on your preferred URL for Dash. dash.campus.edu would be consistent with other campuses, but the final decision is yours.
2. Request CNAMES for development, staging, and production URLs. If you use dash.campus.edu for production, then things should look something like this:
  * dash-dev.campus.edu should resolve to uc3-datashare-dev.cdlib.org, 192.35.209.63
  * dash-stg.campus.edu should resolve to uc3-datashare-stg.cdlib.org, 192.35.209.64
  * dash.campus.edu should resolve to cdl-datashare-p01.ucop.edu, 128.48.120.139
3. We normally use self-signed certificates in development and staging. This eliminates the hassle of managing 'real' certificates, but will result in users in development and staging getting a security alert from their browser. In production we require a proper CA-signed certificate. Please generate a certificate request and private key, and obtain a certificate for dash.campus.edu from your preferred CA. If you would like to avoid the security alerts in development and staging, add dash-dev.campus.edu and dash-stg.campus.edu to your certificate as 'Subject Alternate Names.'

## Shibboleth
To simplify authentication, please work with your campus Shibboleth administrator to make your IdP compliant with the 'Research and Scholarship' category at InCommon. 

  * General information on the R&S category is [here](https://spaces.internet2.edu/display/InCFederation/Research+and+Scholarship+Category)    
  * Specifics for making the campus IdP compliant are [here](https://spaces.internet2.edu/display/InCFederation/Configure+a+Shibboleth+IdP+to+Support+R+and+S) and [here](https://spaces.internet2.edu/display/InCFederation/Identity+Providers+that+Support+R+and+S). 

The R&S configuration will authorize your campus IdP to release to Dash the following user attributes:

    ePPN (eduPersonPersonalName)
    email
and either:

    displayName

or the combination of:

    sn (surname)
    givenName

If your campus Shibboleth administrator does not want to make your IdP part of the Research and Scholarship category, then the campus IdP must be explicitly configured to supply these attributes to the Dash application's Service Provider.

The campus.edu domain administrator at your campus will receive a request from InCommon when CDL adds the campus information to the Shibboleth Service Provider metadata. The campus domain administrator will need to respond to InCommon authorizing the inclusion of the *.campus.edu hostnames within metadata registered by UCOP.

## Logo

1. Determine your campus restrictions/policies around use of logos. Logo regulations for your campus, and for sites hosted by (or appear to be hosted by) your institution. 
2. Provide us with a logo (high resolution, either square/circle or horizontal rectangle in shape). Format should be .eps, .jpg or .png. This logo will go to the right on all of your Dash pages.

## Terms of Use and Privacy Policy

Please be aware that your campus may have rules and regulations about websites they are hosting (or appear to be hosting). You should research whether there are any issues with linking to the CDL [Terms of use](http://www.cdlib.org/about/terms.html) and [Privacy Policy](http://www.cdlib.org/about/privacy.html) from your Dash instance.

## Text Updates

1. Footer: Tell us what phrase and link you would like in the brackets of this footer sentence: Dash is a collaborative project between [XX - e.g., the UCLA library] and the UC Curation Center. 
2. Contact us: Provide us with an email address for who/where the “contact us” form should go.
3. FAQ: Create a campus-specific version. Start with [this text](http://cdluc3.github.io/dash/generic-faq) and amend as necessary.
4. About: Create a campus-specific version. Start with [this text](http://cdluc3.github.io/dash/generic-about) and amend as necessary.

## Seed Datasets

Identify few datasets that can serve as "seed" datasets for your instance of Dash. Share these datasets with us, and we will put them in the Dash collection before your instance goes live. If this is not done, users will log into the Dash system and see no datasets from your institution. 
