##XSD Schema and XML examples 

###Preamble

There are 5 sorts of resources in DASISH: CachedRepresentation, Target, Principal, Annotation, Notebook. Each of them has the corresponding xsd-type in the schema. There is no type with the name CachedRepresentation because a cached representation is a "pure" resource like an image or a text file that does not contain any meta-information about itself. The metadata of a cached presentation are defined via an instance of CachedRepresentationInfo type.

Each of these 5 types has an obligatory attribute "URI" which contains DASISH identifier pointing to the location of the resource on the DASISH server.

Resource-info types TargetInfo, AnnotationInfo, NotebookInfo contain reference to the corresponding resource plus the most important information about the resource. There are corresponding list-of-resource-info types: TargetInfos, AnnotationInfos, NotebookInfos.

There is a number of auxiliary types as well. A commonly-used one is ResourceREF which contains the attribute "ref" of type xs:anyURI. It allows to declare elements-references and avoid mixing them with elements-resources.

Currently the schema is located at [SchemaCat repository](http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd).

### Working with principals 
*GET api/principals/00000000-0000-0000-0000-000000000112*

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<principal xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
URI="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <displayName>Peter</displayName>
    <eMail>Peter.Withers@mpi.nl</eMail>
</principal>
```

*GET api/principals/00000000-0000-0000-0000-0000000000112/current*
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<currentPrincipalInfo xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
ref="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <currentPrincipal>false</currentPrincipal>
</currentPrincipalInfo>
```

*GET api/principals/info?email=​twagoo@mpi.nl*
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<principal xmlns="http://www.dasish.eu/ns/addit" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 URI="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <displayName>Twan</displayName>
    <eMail>Twan.Goosen@mpi.nl</eMail>
</principal>
```

###Retrieving annotations

Responding *GET api/annotations?link=Sagrada*: all annotations which annotating links containing "Sagrada"

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<annotationInfoList xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <annotationInfo ref="https://lux17.mpi.nl/ds/webannotator/api/annotations/00000000-0000-0000-0000-000000000021" ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111">
        <headline>Sagrada Famiglia</headline>
        <lastModified>2013-08-12T09:25:00.383Z</lastModified>
        <targets>
            <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000031</ref>
            <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000032</ref>
        </targets>
    </annotationInfo>
    <annotationInfo ref="https://lux17.mpi.nl/ds/webannotator/api/annotations/d658a511-f1c9-4203-8531-2351b0875c6e" ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113">
        <headline>Sagrada Família - Wikipedia, the free encyclopedia</headline>
        <lastModified>2014-04-01T14:06:04.328613Z</lastModified>
        <targets>
            <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/fa4bbfff-bca7-47cc-ab48-bb68fe943758</ref>
        </targets>
    </annotationInfo>
    <annotationInfo ref="https://lux17.mpi.nl/ds/webannotator/api/annotations/26d7254c-7cb6-4a12-b33b-47ba1769f165" ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113">
        <headline>de author van het idee</headline>
        <lastModified>2014-04-01T15:06:32.587747Z</lastModified>
        <targets>
            <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/d9651f71-42a6-455c-9609-ea856ac227e3</ref>
        </targets>
    </annotationInfo>
    <annotationInfo ref="https://lux17.mpi.nl/ds/webannotator/api/annotations/ceeb6a75-927f-4ffb-a7b9-af11a45beb78" ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113">
        <headline>Sagrada Família - Wikipedia</headline>
        <lastModified>2014-04-01T13:45:49.029405Z</lastModified>
        <targets>
            <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/9d645fa5-026d-49a7-885d-235a5ae8520d</ref>
        </targets>
    </annotationInfo>
</annotationInfoList>
```
*Responding GET api/annotations/00000000-0000-0000-0000-000000000021*

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<annotation xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
URI="https://lux17.mpi.nl/ds/webannotator/api/annotations/00000000-0000-0000-0000-000000000021" 
ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <headline>Sagrada Famiglia</headline>
    <lastModified>2013-08-12T09:25:00.383Z</lastModified>
    <body>
        <textBody>
            <mimeType>text/html</mimeType>
            <body>&lt;html&gt;&lt;body&gt;some html 1&lt;/body&gt;&lt;/html&gt;</body>
        </textBody>
    </body>
    <targets>
        <targetInfo ref="https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000031">
            <link>http://nl.wikipedia.org/wiki/Sagrada_Fam%C3%ADlia#de_Opdracht</link>
            <version>version 1.0</version>
        </targetInfo>
        <targetInfo ref="https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000032">
            <link>http://nl.wikipedia.org/wiki/Antoni_Gaud%C3%AD#Vroege_werk</link>
            <version>version 1.1</version>
        </targetInfo>
    </targets>
    <permissions public="write">
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="write"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000221" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/5c659602-b390-47fa-a762-0a5c1a0be52f" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/c620294a-dbdd-4198-aded-619026ee0513" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/f323d18d-3f86-4625-b47c-35844cedd59c" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/e1788887-50b4-40c2-94a9-98a662d3ef7d" level="read"/>
    </permissions>
</annotation>
```
*GET api/annotations/00000000-0000-0000-0000-000000000021/targets*

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<targetList xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000031</ref>
    <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000032</ref>
</targetList>


```
*GET api/annotations/00000000-0000-0000-0000-000000000021/permissions*
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<permissionList xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
public="write" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="write"/>
    <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113" level="read"/>
    <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000221" level="read"/>
    <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/5c659602-b390-47fa-a762-0a5c1a0be52f" level="read"/>
    <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/c620294a-dbdd-4198-aded-619026ee0513" level="read"/>
    <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/f323d18d-3f86-4625-b47c-35844cedd59c" level="read"/>
    <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/e1788887-50b4-40c2-94a9-98a662d3ef7d" level="read"/>
</permissionList>
```
*GET api/targets/00000000-0000-0000-0000-000000000032*


```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<target xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" URI="https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000032" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <lastModified>2014-03-13T09:52:51.004723Z</lastModified>
    <link>http://nl.wikipedia.org/wiki/Antoni_Gaud%C3%AD#Vroege_werk</link>
    <version>version 1.1</version>
    <siblingTargets>
        <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000032</ref>
    </siblingTargets>
    <cachedRepresentatinons>
        <cached ref="https://lux17.mpi.nl/ds/webannotator/api/cached/00000000-0000-0000-0000-000000000052">
            <fragmentString>Vroeger Werk</fragmentString>
        </cached>
    </cachedRepresentatinons>
</target>
```
*GET api/targets/00000000-0000-0000-0000-000000000032/versions*



An unresolvable target obeys the same schema type. A target becomes unresolvable if e.g. its link becomes obsolete or broken. The respond for an annotation with unresolved targets and the respond for an annotation with resolved targets (see above) are both instances of the same schema element. If the primcipla sees that the client cannot resolve some targets in the requested annotations (e.g., some target fragments are not highlighted) , (s)he may ask for cached representations of the annotated source.

*GET api/cached/00000000-0000-0000-0000-000000000051/metadata*

```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<cashedRepresentationInfo xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" URI="https://lux17.mpi.nl/ds/webannotator/api/cached/00000000-0000-0000-0000-000000000051" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <mimeType>image/png</mimeType>
    <tool>some tool 1</tool>
    <type>image</type>
</cashedRepresentationInfo>
```

For getting an actual cahced-representation file, use 

*GET api/cached/00000000-0000-0000-0000-000000000051/stream*

or 

*GET api/cached/00000000-0000-0000-0000-000000000051/content* (if it is an image)

Additionally,  a client may request the list of all versions of a target.
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<referenceList xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-000000000032</ref>
    <ref>https://lux17.mpi.nl/ds/webannotator/api/targets/00000000-0000-0000-0000-00000000003c</ref>
</referenceList>
```



###Making a new annotation

Request body for *POST api/annotations*


```xml 
<?xml version="1.0" encoding="UTF-8"?>
<annotation xmlns="http://www.dasish.eu/ns/addit"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xhtml="http://www.w3.org/1999/xhtml/"
    xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd" 
    URI="xxx" 
    ownerRef="yyy">
    <headline>X-Pointer test annotation 6667</headline>
    <lastModified>2013-09-29T19:52:28.969+02:00</lastModified>
    <body>
        <xmlBody>
            <mimeType>application/xml+xhtml</mimeType>
            <xhtml:span style="background-color:rgb(0,0,153);color:rgb(255,255,255);border: thick solid rgb(0, 0, 153);">X pointer experiment tmpTarget </xhtml:span>
        </xmlBody>
    </body>
    <targets>
        <targetInfo ref="tmpTarget">
            <link>https://developer.mozilla.org/en-US/docs/Building_an_Extension#xpointer(start-point(string-range(//h2[@id="Create_a_Chrome_Manifest"]/text()[1],'',0))/range-to(string-range(//h2[@id="Create_a_Chrome_Manifest"]/text()[1],'',24)))</link>
            <version>1.0</version>
        </targetInfo>      
    </targets>
    <permissions public="read">
        <permission level = "write" principalRef="http://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112"/>
        <permission level = "write" principalRef="http://lux17.mpi.nl/ds/webannotator/api/princiapls/00000000-0000-0000-0000-000000000111"/>
    </permissions>
</annotation>
```

New-annotation's URI and  the owner reference will generated by the server, and the ones given in the request will be replaced. The new annotation URI is service URI + the UUID generated by the server. The owner reference is the service URI + logged-in user UUID.
The targets's URI will be replaced if the target is new (has not been presented in the dtatabase yet).

Response body (envelope) for *POST api/annotations*


```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<responseBody xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <annotation URI="http://lux17.mpi.nl/ds/webannotator/api/annotations/1d02f393-da25-4246-934c-876222a2d7fb" ownerRef="http://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113">
        <headline>X-Pointer test annotation 6667</headline>
        <lastModified>2014-04-09T12:46:51.754226Z</lastModified>
        <body>
            <xmlBody>
                <mimeType>application/xml+xhtml</mimeType>
                <xhtml:span xmlns:xhtml="http://www.w3.org/1999/xhtml/" style="background-color:rgb(0,0,153);color:rgb(255,255,255);border: thick solid rgb(0, 0, 153);">X pointer experiment 1db0dbe6-ac89-4a4f-ac4c-c8ff764db232 </xhtml:span>
            </xmlBody>
        </body>
        <targets>
            <targetInfo ref="http://lux17.mpi.nl/ds/webannotator/api/targets/1db0dbe6-ac89-4a4f-ac4c-c8ff764db232">
                <link>https://developer.mozilla.org/en-US/docs/Building_an_Extension#xpointer(start-point(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',0))/range-to(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',24)))</link>
                <version>1.0</version>
            </targetInfo>
        </targets>
        <permissions public="read">
            <permission principalRef="http://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="write"/>
            <permission principalRef="http://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" level="write"/>
        </permissions>
    </annotation>
    <actionList>
        <action>
            <object>http://lux17.mpi.nl/ds/webannotator/api/targets/1db0dbe6-ac89-4a4f-ac4c-c8ff764db232</object>
            <message>CREATE_CACHED_REPRESENTATION</message>
        </action>
    </actionList>
</responseBody>
```
As you see, the temporary URIs/references are replaced with permanent references. However, no cahced representation is found for the target. Therefore, in the action part of the envelope there is an action CREATE_CACHED_REPRESENTATION for the object which is the target for the web-page.

The client sends metadata cached representation in the POST body, and a cached representation itself. An example of serialized metadata for a cached representation has been considered above, so we do not give it here.

###Editing an annotation

PUT *api/annotations/1d02f393-da25-4246-934c-876222a2d7fb*

Since the complete update of the annotation assumes also changing the premissions, this request can be perforemd only by the owner of the annotation.

Request body : an updated annotation

```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<annotation xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
URI="https://lux17.mpi.nl/ds/webannotator/api/annotations/1d02f393-da25-4246-934c-876222a2d7fb" 
ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <headline>update X-Pointer test annotation 6667</headline>
    <lastModified>2014-04-09T12:46:51.754226Z</lastModified>
    <body>
        <xmlBody>
            <mimeType>application/xml+xhtml</mimeType>
            <xhtml:span xmlns:xhtml="http://www.w3.org/1999/xhtml/" style="background-color:rgb(0,0,153);color:rgb(255,255,255);border: thick solid rgb(0, 0, 153);">update X pointer experiment 1db0dbe6-ac89-4a4f-ac4c-c8ff764db232 </xhtml:span>
        </xmlBody>
    </body>
    <targets>
        <targetInfo ref="https://lux17.mpi.nl/ds/webannotator/api/targets/1db0dbe6-ac89-4a4f-ac4c-c8ff764db232">
            <link>https://developer.mozilla.org/en-US/docs/Building_an_Extension#xpointer(start-point(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',0))/range-to(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',24)))</link>
            <version>1.0</version>
        </targetInfo>
    </targets>
    <permissions public="none">
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" level="read"/>
    </permissions>
</annotation>
```

Enveloped respond containing new (updated) annotation and a list of actions:

```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<responseBody xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <annotation URI="https://lux17.mpi.nl/ds/webannotator/api/annotations/1d02f393-da25-4246-934c-876222a2d7fb" ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113">
        <headline>update X-Pointer test annotation 6667</headline>
        <lastModified>2014-04-09T12:58:32.793453Z</lastModified>
        <body>
            <xmlBody>
                <mimeType>application/xml+xhtml</mimeType>
                <xhtml:span xmlns:xhtml="http://www.w3.org/1999/xhtml/" style="background-color:rgb(0,0,153);color:rgb(255,255,255);border: thick solid rgb(0, 0, 153);">update X pointer experiment 1db0dbe6-ac89-4a4f-ac4c-c8ff764db232 </xhtml:span>
            </xmlBody>
        </body>
        <targets>
            <targetInfo ref="https://lux17.mpi.nl/ds/webannotator/api/targets/1db0dbe6-ac89-4a4f-ac4c-c8ff764db232">
                <link>https://developer.mozilla.org/en-US/docs/Building_an_Extension#xpointer(start-point(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',0))/range-to(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',24)))</link>
                <version>1.0</version>
            </targetInfo>
        </targets>
        <permissions public="none">
            <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="read"/>
            <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" level="read"/>
        </permissions>
    </annotation>
    <actionList>
        <action>
            <object>https://lux17.mpi.nl/ds/webannotator/api/targets/1db0dbe6-ac89-4a4f-ac4c-c8ff764db232</object>
            <message>CREATE_CACHED_REPRESENTATION</message>
        </action>
    </actionList>
</responseBody>
```
*PUT api/annotations/1d02f393-da25-4246-934c-876222a2d7fb/body*

The request can be peformed by a "writer".

Request body:

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<annotationBody xmlns="http://www.dasish.eu/ns/addit"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xhtml="http://www.w3.org/1999/xhtml/" 
    xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
        <xmlBody>
            <mimeType>application/xml+xhtml</mimeType>
            <xhtml:span style="background-color:rgb(0,0,153);color:rgb(255,255,255);border: thick solid rgb(0, 0, 153);">2 UPDATE X pointer experiment UPDATE body </xhtml:span>
      </xmlBody>
```
Response:

```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<responseBody xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <annotation URI="https://lux17.mpi.nl/ds/webannotator/api/annotations/1d02f393-da25-4246-934c-876222a2d7fb" ownerRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000113">
        <headline>update X-Pointer test annotation 6667</headline>
        <lastModified>2014-04-09T13:01:21.900643Z</lastModified>
        <body>
            <xmlBody>
                <mimeType>application/xml+xhtml</mimeType>
                <xhtml:span xmlns:xhtml="http://www.w3.org/1999/xhtml/" style="background-color:rgb(0,0,153);color:rgb(255,255,255);border: thick solid rgb(0, 0, 153);">2 UPDATE X pointer experiment UPDATE body </xhtml:span>
            </xmlBody>
        </body>
        <targets>
            <targetInfo ref="https://lux17.mpi.nl/ds/webannotator/api/targets/1db0dbe6-ac89-4a4f-ac4c-c8ff764db232">
                <link>https://developer.mozilla.org/en-US/docs/Building_an_Extension#xpointer(start-point(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',0))/range-to(string-range(//h2[@id=&quot;Create_a_Chrome_Manifest&quot;]/text()[1],'',24)))</link>
                <version>1.0</version>
            </targetInfo>
        </targets>
        <permissions public="none">
            <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="read"/>
            <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" level="read"/>
        </permissions>
    </annotation>
    <actionList>
        <action>
            <object>https://lux17.mpi.nl/ds/webannotator/api/targets/1db0dbe6-ac89-4a4f-ac4c-c8ff764db232</object>
            <message>CREATE_CACHED_REPRESENTATION</message>
        </action>
    </actionList>
</responseBody>
```
*PUT api/annotations/1d02f393-da25-4246-934c-876222a2d7fb/permissions* (performed by the owner)

Supplementary updating the list of permissions in the annotation. If the principal is listed in this body,  her/his access level is updated accrording to what is given in the body.

Request body:

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<permissionList xmlns="http://www.dasish.eu/ns/addit"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd"
    public="none">
    <permission level="write" principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112"/>
    <permission level="read" principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000114"/>
</permissionList>
```
Respond

```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<responseBody xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <permissions public="none">
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="write"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000114" level="read"/>
    </permissions>
    <actionList/>
</responseBody>
```
Now, assume that principal 00000000-0000-0000-0000-000000000114 is not known to the DASISH data base then respond bey would be:

Respond

```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<responseBody xmlns="http://www.dasish.eu/ns/addit" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <permissions public="none">
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000111" level="read"/>
        <permission principalRef="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000112" level="write"/>
    </permissions>
    <actionList>
        <action message="PROVIDE_USER_INFO" object="https://lux17.mpi.nl/ds/webannotator/api/principals/00000000-0000-0000-0000-000000000114"/>
    </actionList>
    </responseBody>
```
PUT *api/annotations/1d02f393-da25-4246-934c-876222a2d7fb/permissions/00000000-0000-0000-0000-000000000114*

Peforemd by the owner.

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<access xmlns="http://www.dasish.eu/ns/addit"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">write</access>
```
Response: string "1 rows are updated/added".

###Managing Notebooks (obsolete section)

*GET api/notebooks*

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<notebooks xmlns="http://www.dasish.eu/ns/addit"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd">
    <notebook ref="http://dasish.eu/notebooks/NIDxyxy">
        <title>Gaudi</title>
    </notebook>
    <notebook ref="http://dasish.eu/notebooks/NIDxefef">
        <title>Douglas Adams</title>
    </notebook>
</notebooks>
```
*GET api/notebooks/NIDxyxy*

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<notebook xmlns="http://www.dasish.eu/ns/addit"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://lux17.mpi.nl/schemacat/schemas/s15/files/dwan.xsd" 
 ref="http://dasish.eu/notebooks/NIDxyxy">
    <title>Gaudi</title>
</notebook>
```
*GET api/notebooks/NIDxyxy/annotations/*

Respond is a list of annotation info, is similar to the respond on *GET api/annotations?link="http://en.wikipedia.org/wiki/Sagrada_Fam%C3%ADlia"&access=read*

###Issues with the schema

As regards all future schema updates, remember to update all available scenario xml documents on  the gGitHub accordingly, and preferably, with as little delay as possible. Validate all of these documents against the revised schema with a reliable XML parser like e.g. the Xerces-J XML parser. Also, if you like, you can check by validating some of our current "real-life" mock xml documents that we have been using for [client development](https://trac.clarin.eu/browser#DASISH/t5.6/client/trunk/chrome/markingcollection/content/markingcollection/annotator-service/test/mockjax/mocks).

###Cached Representations' BLOBs

For the back-end (and the database!): the cached representation for now is stored in the database as a BLOB. See [postrges documentation on blobs](http://dba.stackexchange.com/questions/803/blobsor-references-in-postgresql/815#815).

