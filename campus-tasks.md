---
layout: page
title: Dash Implementation Tasks
permalink: /campus-tasks/
---

## Certificates
1. Decide on your preferred URL for Dash. dash.institution.edu would be consistent with other Dash instances, but the final decision is yours.
2. Request CNAMES for development, staging, and production URLs. If you use dash.institution.edu for production, then things should look something like this:
  * dash-dev.institution.edu should resolve to uc3-datashare-dev.cdlib.org
  * dash-stg.institution.edu should resolve to uc3-datashare-stg.cdlib.org
  * dash.institution.edu should resolve to cdl-datashare-p01.ucop.edu
3. We normally use self-signed certificates in development and staging. This eliminates the hassle of managing 'real' certificates, but will result in users in development and staging getting a security alert from their browser. In production we require a proper CA-signed certificate. Please generate a certificate request and private key, and obtain a certificate for dash.institution.edu from your preferred CA. If you would like to avoid the security alerts in development and staging, add dash-dev.institution.edu and dash-stg.institution.edu to your certificate as 'Subject Alternate Names.'

## Shibboleth
To simplify authentication, please work with your institution's Shibboleth administrator to make your IdP compliant with the 'Research and Scholarship' category at InCommon. 

  * General information on the R&S category is [here](https://spaces.internet2.edu/display/InCFederation/Research+and+Scholarship+Category)    
  * Specifics for making the institution IdP compliant are [here](https://spaces.internet2.edu/display/InCFederation/Configure+a+Shibboleth+IdP+to+Support+R+and+S) and [here](https://spaces.internet2.edu/display/InCFederation/Identity+Providers+that+Support+R+and+S). 

The R&S configuration will authorize your institution IdP to release to Dash the following user attributes:

    ePPN (eduPersonPersonalName)
    email
and either:

    displayName

or the combination of:

    sn (surname)
    givenName

If your institution Shibboleth administrator does not want to make your IdP part of the Research and Scholarship category, then the institution IdP must be explicitly configured to supply these attributes to the Dash application's Service Provider.

The institution.edu domain administrator at your institution will receive an email from InCommon when CDL adds the institution information to the Shibboleth Service Provider metadata. The institution domain administrator will need to respond to InCommon authorizing the inclusion of the *.institution.edu hostnames within metadata registered by UCOP.

## Logo

1. Determine your institution restrictions/policies around use of logos. Logo regulations for your institution, and for sites hosted by (or appear to be hosted by) your institution. 
2. Provide us with a logo (high resolution, either square/circle or horizontal rectangle in shape). Format should be .eps, .jpg or .png. This logo will appear on all of your Dash pages.

## Terms of Use and Privacy Policy

Please be aware that your institution may have rules and regulations about websites they are hosting (or appear to be hosting). You should research whether there are any issues with linking to the CDL [Terms of use](http://www.cdlib.org/about/terms.html) and [Privacy Policy](http://www.cdlib.org/about/privacy.html) from your Dash instance.

## Text Updates

1. Footer: Tell us what phrase and link you would like in the brackets of this footer sentence: Dash is a collaborative project between [XX - e.g., the UCLA library] and the UC Curation Center. 

