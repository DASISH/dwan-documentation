##Short how-to for DWAN wired-marker-based client

###Installation

Go to git-hub [GitHub's DASISH/dwan-client-wiredmarker repository](https://github.com/DASISH/dwan-client-wiredmarker) to download the extension. Follow the instructions and read the wiki-page referred from there. 

###Working with the client.
#### The first appearance
When the extension is properly installed and enabled you see the following screen:
![Before login](images/dwan-wired-marker/1_before_login.png)
#### Login
To have access to the database, that enables reading and posting annotations, you need to log-in.  Now we describe how to log-in if your institution is listed as a Shibboleth identity provider. Then you can just use your institution credentials.
* First, press "login" button and choose your institution or clarin as an identity provider.
![choose idp](/images/dwan-wired-marker/2_login_idp.png)
* Second, provide your credentials and click "Login".
![Credentials](/images/dwan-wired-marker/3_logging_in.png)

#### Seeing annotations of colleagues
They are listed in the incoming directory. Click "incoming". (If it is your first dwan-session with the page annotation of which you want to see, you need to browse to it.) Click on the annotation you want to see. It must appear on the web-page in the light-yellow colour. Unless it appears, refresh the page.

![Get an annotation made by your colleague](images/dwan-wired-marker/4_incoming.png)

#### Getting your annotations

Annotations made by you are to be seen in the coloured folders according to the colours with which you have marked annotated texts. Click on the annotation you want to see. 

![Get an annotation made by you](images/dwan-wired-marker/5_myannotation.png)

#### Unresolvable annotated source
If you want to see your or someonelse's annotation, and it does not appear after cliking on it and refreshing the page, it means that the client cannot resolve the annotated fragment. The most probable reason for it is that the web-page has been changed since it was annotated. Point the mouse to the annotation (in the list at the left-hand side) in question and righ-click. In the pop-up menu select "Cached representations" and click "open remote cache" in the sub-menu. You will see the cached annotation:

![Get a cached representation](images/dwan-wired-marker/10_unresolvable_2_cached.png)

Compare this example cached representation with the example current web-page below, the annotation on which cannot be found:

![Updated web-page](images/dwan-wired-marker/9_unresolvable_1.png)

As you see the annotated sentence has been changed.

#### Posting an annotation 

* Go to the web-page you want to annotate, select a text fragment by the mouse and obtain the marker's colour menu by right-clicking the mouse:

![Make annotation 1](images/dwan-wired-marker/6_make_annotation_1.png)


* Select the colour by left-clicking the mouse, and fill in the fields in the text-box for making an annotation.

![Make annotation 2](images/dwan-wired-marker/7_make_annotation_2.png)

* Click  "OK" in the box when you are done. The annotation should be shown on the page:

![Make annotation 3](images/dwan-wired-marker/8_make_annotation_3.png)
