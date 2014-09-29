---
layout: page
title: Procedure to add campus
permalink: /procedure-to-add-campus/
---

This procedure assumes that the campus has already set up DNS entries and provided certificates per the instructions for campus integration.

1. Install the campus-provided certificates under /dash/ssl/[certificate expiration date] for each environment. The date should be in the form YYYY-MM-DD.

2. Add a Discovery Response endpoint to the Shibboleth metadata for each environment (dev/stg/production)

example: https://dash-dev.lib.uci.edu/Shibboleth.sso/Login

3. Add Assertion Consumer Service endpoints for SAML 2.0 Browser Post, SAML 2.0 Browser Artifact, SAML 1.0 Browser Post, and SAML 1.0 Browser Artifact to the Shibboleth metadata for each environment (dev/stg/production)

examples:

Index: 25
Type: urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST
Location: https://dash.ucmerced.edu/Shibboleth.sso/SAML2/POST
Index: 26
Type: urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Artifact
Location: https://dash.ucmerced.edu/Shibboleth.sso/SAML2/Artifact
Index: 27
Type: urn:oasis:names:tc:SAML:1.0:profiles:browser-post
Location: https://dash.ucmerced.edu/Shibboleth.sso/SAML/POST
Index: 28
Type: urn:oasis:names:tc:SAML:1.0:profiles:artifact-01
Location: https://dash.ucmerced.edu/Shibboleth.sso/SAML/Artifact

4. For each environment, edit the correct .yaml file for the host to set up the Vhost using Puppet. The .yaml files are best edited as dpr2@uc3-mrt-wrk1-stg.cdlib.org. The files live under /dpr2/etc/infra-puppet/hiera/node/[fqdn].yaml. This is most easily accomplished by copy-and-pasting an existing campus configuration block.

Example:

/dpr2/etc/infra-puppet/hiera/node/uc3-datashare-dev.cdlib.org.yaml

  vhost_ucla:
    path: "apps/apache/conf"
    script_type: template
    user: "dash"
    script: "vhost-dash-ucla-dev.cdlib.org.conf"
    mytemplate: "vhost-dash-dev.conf"
    myvhostname: "dash-ucla-dev.cdlib.org"
    mydocroot: "/dash/apps/apache/htdocs/dev.dash.ucla.edu"
    mycert: "/dash/ssl/2017-08-17/dash_ucla_edu_cert.cer"
    mykey: "/dash/ssl/2017-08-17/dash.ucla.edu-san.key"
    myidpshort: "ucla"
    myothercampuses:
      - { myothercampusidp: "urn:mace:incommon:ucop.edu", myothercampushost: dash-dev.ucop.edu }
      - { myothercampusidp: "urn:mace:incommon:berkeley.edu", myothercampushost: dash-dev.berkeley.edu }
    permissions: "0644"

5. Update the 'myothercampuses' field for all the other campuses to include the new campus.

6. Be certain the campus setup data in the .yaml file exists under both the section for Dash and the section for Root usage. Copy-and-paste the finished configuration block.

7. Do a git commit and push to send the new .yaml file to the git repository master. A script called /dpr2/bin/push.bash automates this process. Just provide a commit message.

8. Log on to each Dash server as the dash user and do the following:

cd /dash/etc/infra-puppet
git pull
/dash/bin/commit.bash

This will pull in the Puppet configuration created in steps 4-7, create the new campus vhost, and update the vhost-base.conf file to include the new campus vhost.

9. /dash/apps/apache/bin/apachectl restart to read in the new config. The new campus site should now be active.
