---
title: "Trust Company Certificate In Firefox"
date: "2018-12-29 11:06"
categories: [firefox, company certificate]
---

By default, the Firefox doesn't trust the company's certificate, that may cause user will recieve certificate error, and unable to view the site.  
However, we can manually configure the Firefox to trust the company certificate to resolve the issue.
* Open Firefox config page by run `about:config` and click "I accept the risk!" to continue
  * Changed the value of entry `security.enterprise_roots.enabled` to **true**
* Export the company **root certificate**
  * Use [portecle](http://portecle.sourceforge.net/) to export the certificate as PEM file
* Open the Firefox option page
  * Navigate to `Certificates` section
  * Click the `View Certificates` button to open the **Certificate Manager** window
  * Import the PEM certificate exported in above step, click the **OK** button to take effect

Now, the Firefox will trust the company certificate.
