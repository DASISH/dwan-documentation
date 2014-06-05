## Web-annotator/API interaction scenarios

### Authentication api/authentication/login 

If a principal logs-in to the annotation service, ```prid``` gets known by the server. Principal's information can be seen at e.g. 
*GET api/principals/00000000-0000-0000-0000-000000000112* via her/his ID, or, for the logged in principal, *GET api/authentication/principal*.

### Visiting an annotated web page

* Principal: visits the page http://en.wikipedia.org/wiki/Sagrada_Fam%C3%ADlia (for example).
* Client: requests the lists of annotations to which the principal has "read" access.

 *GET api/annotations?link=http://en.wikipedia.org/wiki/Sagrada_Fam%C3%ADlia&access=read*
* Service: returns list of annotation info: URI-s with the corresponding headlines, owners, and target source refs (URI-s);

See the example [getting annotations for Sagrada Famiglia wiki-page](examples.md#responding-get-apiannotationslinksagrada).

If the client cannot fit annotated fragments into the current version of the document, the corresponding target source is called unresolved. Unresolvability of a target source triggers the client-side workflow of getting a cached representation of the annotated version of the document.

### Viewing an individual annotation

**Resolvable target**

* Principal: selects an annotation (with resolvable targets) for reading.
* Client: retrieves the annotation GET api/annotations/```aid```
* Service: returns the annotation

See the example of [getting an annotation in examples](examples.md#responding-get-apiannotations00000000-0000-0000-0000-000000000021).

**Unresolvable target**

* Principal: selects an annotation with unresolvable targets for reading.
* Client: get annotation GET api/annotations/```aid```
* Client: does show the annotated web-document, but does not show the annotation because the annotated fragment(s) cannot be resolved. Refreshing the page does not help.
* Principal: requests a cached representation of the annotation, e.g. "Cached representations --> get remote cache".
* Client: get the cached representation for the considered version GET api/cached/```cid```/stream.


 
 
**Annotation creation**
* Principal: creates a text note on a selected text.
* Client: sends the annotation to the server *POST api/annotation*. See an example of [the body of the POST a new annotation in examples](examples.md#request-body-for-post-apiannotations).
* Service: responds with the envelope: {*annotation-new*, *Actions*}. Here *annotation-new* is the serialisation of the newly-created in the DB annotation obtained from the POSTed new *annotation* by replacing all its temporary target- id-s with the corresponding actual references, which are URI's in the DB. The list of actions may be empty or contain "CREATE_CACHED_REPRESENTATION". See a [response envelope upon creating a new annotation in examples](examples.md#response-body-envelope-for-post-apiannotations).

* Client: sends cached representation POST/api/targets/```tid```/fragmet/```fragmentdescriptor```/cached
* Service: stores representation

**Editing an annotation body**

*PUT api/annotations/```aid```/body*

Request body: XML new body *annotation*, see ["updated annotation" in examples](examples.md#request-body--an-updated-annotation). Response is an envelope as for posting, also [see examples](examples.md#enveloped-respond-containing-new-updated-annotation-and-a-list-of-actions).

###Managing permission lists of permissions

A permission is a pair (principal reference, access), where access is "read" or "write".

**Give the list of the permissions for a given annotation/notebook**

*GET api/annotations/```aid```/permissions*

Response: see List of permissions for a given annotation, see [examples](examples.md#get-apiannotations00000000-0000-0000-0000-000000000021permissions).

**Adding and deleting principals in permission lists**

*GET api/principals/info?email=[[...]]*

Response: Principal (her/his uri, display name, e-mail), see getting principal via his/her e-mail, see [examples](examples.md#get-apiprincipalsinfoemailtwagoompinl). If a principal with the given e-mail does not exist, status 404 is returned.

*PUT api/annotations/```aid```/permissions*

Request body contains the list of permissions, see "update permission list" in [examples](examples.md#put-apiannotations1d02f393-da25-4246-934c-876222a2d7fbpermissions). Response is the envelope.

**Adding a principal with a certain access**

*PUT api/annotations/```aid```/permissions/```prid```*

Request body contains the access level of this user to this annotation, see "adding/updating a principal with a specific permission", see [examples](examples.md#put-apiannotations1d02f393-da25-4246-934c-876222a2d7fbpermissions00000000-0000-0000-0000-000000000114). No enveloped response, just an http status code.

**Removing a reader or a writer**

*DELETE api/annotations/```aid```/permissions/```prid```*

No enveloped response, just an http status code

##Managing annotations

**Deleting an entire annotation (if logged-in ```prid``` is the owner)**

*DELETE api/annotations/```aid```*

No enveloped response, just an http status code.

##Notebooks (obsolete api)

**Retrieve notebooks Info**

*GET api/notebooks*

Response: the list of notebook infos, see Retrieving notebook info list.

**Retrieve notebook info**

*GET api/notebooks/```nid```*

Response: Notebook Info, see Retrieving notebook info.

**Retrieving the list of annotations in a notebook if ```prid``` has a read access to this notebook**

*GET api/notebooks/```nid```/annotations/*

Response: the list of annotation Info, see Retrieving the list of annotations for a notebook.

**Adding an annotation to a notebook**

*PUT api/notebooks/```nid```/```aid```*

Request body: empty. Response: only a http status code.
