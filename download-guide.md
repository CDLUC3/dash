---
layout: page
title: Guidance for Downloading Data
permalink: /download-guide/
---


_**To find data**, see our [User Guide](http://cdluc3.github.io/dash/user-guide). You do not need to log into Dash to search, browse, or download data._

### From the Dataset landing page, click "Download".

![landing page 2](https://raw.githubusercontent.com/CDLUC3/dash/gh-pages/images/userguide/landing2.jpg)

1. Depending on your browser's download settings, either your dataset package will automatically download you will be asked to save the package on your computer. The file name will be similar to ````ark+=b7280=d1059f_version_7.zip````.
   * ````ark+=b7280=d1059f````: internal identifier assigned to the data package
    * ````version_7````: the version number of the data package you are downloading
1. Double click on the .zip file to view its contents. The new folder's name will reflect the version number, e.g., ````v007```` 
1. Open the "full" folder.
1. Open the "producer" folder. The data files will be in this folder.

![files](https://raw.githubusercontent.com/CDLUC3/dash/gh-pages/images/userguide/files.jpg)

All other files are related to the deposit and harvest of data from the [Merritt repository](http://merritt.cdlib.org). 

  * in the "system" folder:
    * mrt-dc.xml: metadata for the dataset ([Dublin Core](http://dublincore.org/) format)
    * mrt-erc.txt: Electronic Resource Citation ([ERC](http://dublincore.org/groups/kernel/spec/)) metadata for the dataset
    * mrt-ingest.txt: Technical information describing the parameters of the Merritt ingest process for this dataset
    * mrt-membership.txt: Merritt collection membership for the dataset
    * mrt-mom.txt: Merritt object properties for the dataset
    * mrt-owner.txt: Administrative owner of the dataset in Merritt
    * mrt-object-map.ttl: Object Reuse and Exchange ([OAI-ORE](http://www.openarchives.org/ore/)) structural metadata  for the dataset
  * in the "producer" folder:
    * mrt-datacite.xml: metadata for the dataset ([DataCite](http://datacite.org) format)
    * mrt-dc.xml: metadata for the dataset ([Dublin Core](http://dublincore.org/) format)
    * mrt-dataone-manifest.txt: Mapping file needed for the submission of the dataset into the Merritt [DataONE](http://dataone.org) member node
  * manifest.txt

### Contents of the README.txt (automatically added to the data package)

The digital object you have downloaded from Merritt contains the dataset as well as a number of system files and folders. In order to access the dataset:

1. You'll see a folder named "v00X" corresponding to the version number of the digital object. Open this folder.
2. Open the "full" folder.
3. Open the "producer" folder. You will find the data here.

More information on folders, files and naming conventions in Merritt objects can be found in the "D-flat" specification: [confluence.ucop.edu/display/Curation/D-flat](https://confluence.ucop.edu/display/Curation/D-flat). Please contact us at uc3@ucop.edu with any questions. 