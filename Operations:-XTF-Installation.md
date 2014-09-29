### Follow these steps to clone Dash XTF repository to your local environment

1. Download XTF Tutorial package: [http://xtf.cdlib.org/download/](http://xtf.cdlib.org/download/)
1. Unzip files to your local server. Will create a directory at ````/xtfWorkshop````
1. Delete XTF directory at ````/xtfWorkshop/tomcat/webapps/xtf````
1. Clone Dash repository from Github:

    ````
        cd xtfWorkshop/tomcat/webapps
        git clone git://github.com/CDLUC3/dash-xtf.git
    ````

### Add exclusions to git index
1. Add these lines to xtfWorkshop/tomcat/webapps/dash-xtf/.git/info/exclude:

   ````
       xtf/data
       xtf/index
   ````
1. Run these commands at the repo home directory:

   ````
       git update-index --assume-unchanged xtf/conf/textIndexer.conf
       git update-index --assume-unchanged xtf/style/crossQuery/queryParser/default/queryParser.xsl
       git update-index --assume-unchanged xtf/style/dynaXML/docReqParser.xsl
   ````



### Download Data directory
1. : Unzip [dash-data.zip](https://github.com/CDLUC3/dashdocs/blob/master/dash-data.zip?raw=true) and rename folder "dash-data" to "data" to 

    ````
        /xtfWorkshop/tomcat/webapps/dash/xtf/
    ````

### Files to change
**For PCs:** 

1. /xtfWorkshop/setVars.bat (line 20)

    ````
        set XTF_HOME=%CATALINA_HOME%\webapps\dash-xtf\xtf
    ````

**For Macs:**  

1. /xtfWorkshop/textIndexer (line 5)

    ````
        export XTF_HOME="$XTFWS/tomcat/webapps/dash-xtf/xtf"
    ````

1. /xtfWorkshop/cmdPrompt.command (line 16)

    ````
        echo "export XTF_HOME=\"$XTFWS/tomcat/webapps/dash-xtf/xtf\"" >> /tmp/xtfworkshop_init
    ````
1. /xtfWorkshop/tomcat.command (line 11)

    ````
        export XTF_HOME="$XTFWS/tomcat/webapps/dash-xtf/xtf"
    ````

**For both PCs and Macs**

1. /xtfWorkshop/tomcat/webapps/dash-xtf/xtf/conf/textIndexer.conf (lines 12 and 13)
        
    ````
        <src path="./data" scan="all"/>
        <db path="./index"/>
    ````


1. /xtfWorkshop/tomcat/webapps/dash-xtf/xtf/style/crossQuery/queryParser/default/queryParser.xsl (line 80)
      
    ````
        <query indexPath="index" termLimit="1000" workLimit="1000000" style="{$stylesheet}" startDoc="{$startDoc}" maxDocs="{$docsPerPage}">
    ````

1. /xtfWorkshop/tomcat/conf/server.xml (line 128)

    ````
        <Host name="localhost"  appBase="webapps/dash-xtf"
    ````

1. /xtfWorkshop/tomcat/webapps/dash-xtf/xtf/style/dynaXML/docReqParser.xsl
  1. line 105
      
    ````
        <xsl:variable name="file" select="concat('data/',$docId)"/>
    ````

  1. line 171

    ````
        <source path="{concat('data/',$docId)}"/>
    ````

1. Follow directions at http://xtf.cdlib.org/getting-started-tutorials/quick-start/:
  * set paths and environment variables with cmdPrompt.bat (PCs) or cmdPrompt.command (Macs)
  * index data with textIndexer
  * start tomcat
  * go to localhost
