###############################################
RESTful Application Programming Interface (API)
###############################################
The REST API allows third-party applications to retrive data stored within
BIGSdb databases.  To use the REST API, your application will make a HTTP
request and parse the response.  The response format is JSON.  

*********
Resources (under development)
*********
* :ref:`/ or /db<db_no_arg>`
* :ref:`/db/{database}<db>`

.. _db_no_arg:

.. index::
   single: API resources; /db [no argument]
   single: API resources; /
   
/ or /db
========
Lists database resources available using the API.

**Supported methods:** GET, POST

**Required query parameters:** None

**Optional query parameters:** None

**Example request URI:** http:/rest.pubmlst.org/

**Response:** List of resource groupings (ordered by name).  Groups may consist
of paired databases for sequence definitions and isolate data, or any set of
related resources.  Each group contains:

* name [string] - short name (usually a single word)
* description [string] - fuller description
* databases [array] - list of database objects, each consists of three 
  key/value pairs:

   * name [string] - name of database config
   * description [string] - short description of resource
   * href [string] - URI to access resource
   
.. _db:

.. index::
   single: API resources; /db

/db/{database}
==============
Lists resources available for specified database configuration.  These will 
vary depending on whether the resource is an isolate or a sequence definition
database.

**Supported methods:** GET, POST

**Required query parameter:** Database configuration name [string]

**Optional parameters:** None

**Example request URI:** http:/rest.pubmlst.org/db/pubmlst_neisseria_isolates

**Response:** Object containing a subset of the following key/value pairs:

* fields [string] - URI to isolate provenance field information
* isolates [string] - URI to isolate records
* schemes [string] - URI to list of schemes
* loci [string] - URI to list of loci
* records [number] - count of available records


**************
Authentication
**************
Protected resources, i.e. those requiring a user to log in, can be accessed via
the API using OAuth (1.0A) authentication (see 
`IETF RFC5849 <http://tools.ietf.org/html/rfc5849>`_ for details).  Third-party
client software has to be registered with the BIGSdb site before they can 
access authenticated resources. The overall three-legged flow works as follows:

#. :ref:`Developer signs up <get_consumer_key>` and gets a consumer key and 
   consumer secret specific to their application.
#. Application :ref:`gets a request token <get_request_token>` and directs user
   to authorization page on BIGSdb.
#. BIGSdb :ref:`asks user for authorization <get_user_authorization>` for 
   application to access specific resource using their credentials.  A verifier
   code is provided.
#. The application exchanges the request token and OAuth verifier code for an 
   :ref:`access token and secret <get_access_token>` (these do not expire but 
   may be revoked by the user or site admin). 
#. Application uses access token/secret to 
   :ref:`request session token <get_session_token>` (this is valid for 12 
   hours).
#. All calls to 
   :ref:`access protected resources <accessing_protected_resources>` are signed
   using the session token/secret and consumer key/secret.
   
It is recommended that application developers use an OAuth library to generate
and sign requests.

.. _get_consumer_key:

.. index::
   single: API authentication; consumer key

Developer sign up to get a consumer key
=======================================
Application developers should apply to the site administrator of the site 
running BIGSdb.  The administrator can 
:ref:`generate a key and secret<create_client_credentials>` using a script - 
both of these will need to be used by the application to sign
requests.

The client id is usually a 24 character alphanumeric string.  The secret is
usually a 42 character alphanumeric (including punctuation) string, e.g.

 * **client_id:** efKXmqp2D0EBlMBkZaGC2lPf
 * **client_secret:** F$M)_+fQ2AFFB2YBDfF9fpHF^qSWJdmmN%L4Fxf5Gur3

.. _get_request_token:

.. index::
   single: API authentication; request token

Getting a request token
=======================

* **Relative URL:** /oauth/get_request_token
* **Supported methods:** GET, POST
 
The application uses the consumer key to obtain a request token.  The request
token is a temporary token used to initiate user authorization for the 
application and will expire in 60 minutes.  The request needs to contain the
following parameters and to be signed using the consumer secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970)
    * this must be within 600 seconds of the current time.
 * oauth_callback ('oob' for desktop applications)
 * oauth_nonce (random string)
 * oauth_version ('1.0')

If the application has been registered and has been granted permission to
access the specific resource, a JSON response will be returned containing the
following parameters:

 * oauth_token
    * This is the request token.  It is usually a 32 character alphanumeric
      string.
    * e.g. fKFm0WNhCfbEX8zQm6qhDA8K23FOWDGE
 * oauth_token_secret
    * This is the secret associated with the request token.  It is usually a 
      32 character alphanumeric string.
    * e.g. aZ0fncP7i5w5jlebdK5zyQ4vrRRVcdnv
 * oauth_callback_confirmed
    * This parameter is always set to true.

.. _get_user_authorization:

.. index::
   single: API authentication; user authorization
   
Getting user authorization
==========================
Once a request token has been obtained, this can be used by the end user to
grant permission to access a specific resource to the application.  The 
application should direct the user to the client authorization page 
(authorizeClient) specific to a database within BIGSdb, e.g. 
http://pubmlst.org/cgi-bin/bigsdb/bigsdb.pl?db=pubmlst_neisseria_seqdef&page=authorizeClient&oauth_token=fKFm0WNhCfbEX8zQm6qhDA8K23FOWDGE

The user will be asked if they wish to grant access to the application on their
behalf:

.. image:: /images/rest/authorize_client.png

If they authorize the access, they will be presented with a verifier code.  
This should be entered in to the client application which will use this 
together with the request token to request an access token.

.. image:: /images/rest/authorize_client2.png

The verifier code is valid for 60 minutes.

.. _get_access_token:

.. index::
   single: API authentication; access token

Getting an access token
=======================
* **Relative URL:** /oauth/get_access_token
* **Supported methods:** GET, POST
 
The application uses the request token, verifier code and its consumer key to 
obtain an access token.  The access token does not expire but can be revoked
by both the end user or the site admininstrator.  The request needs to contain
the following parameters and to be signed using the consumer secret and request
token secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_token (request token)
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970)
    * this must be within 600 seconds of the current time.
 * oauth_nonce (random string)
 * oauth_version ('1.0')

If the application has been registered and has been granted permission to
access the specific resource, a JSON response will be returned containing the
following parameters:

 * oauth_token
    * This is the access token.  It is usually a 32 character alphanumeric
      string.
    * e.g. SDrC74ZVl5SYSqY8lWZqrRxnyDnNGVFO
 * oauth_token_secret
    * This is the secret associated with the access token.  It is usually a 
      32 character alphanumeric string.
    * e.g. tYI2SPzgiO02IRVzW4JR1ez6Vvm4gVyv
    
.. _get_session_token:

.. index::
   single: API authentication; session token

Getting a session token
=======================
* **Relative URL:** /oauth/get_session_token
* **Supported methods:** GET, POST

The application uses the access token and its consumer key to obtain a session
token.  The session token is valid for 12 hours before it expires.  The request
needs to contain the following parameters and to be signed using the consumer
secret and access token secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_token (access token)
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970)
    * this must be within 600 seconds of the current time.
 * oauth_nonce (random string)
 * oauth_version ('1.0')

If the application has been registered and has been granted permission to
access the specific resource, a JSON response will be returned containing the
following parameters:

 * oauth_token
    * This is the session token.  It is usually a 32 character alphanumeric
      string.
    * e.g. H8CjIS8Ikq6hwCUqUfF1l4pTaCYl8Ljw
 * oauth_token_secret
    * This is the secret associated with the session token.  It is usually a 
      32 character alphanumeric string.
    * e.g. RfponbaNPO7tkZ2miHFISk0pMndePNfJ
    
.. _accessing_protected_resources:

.. index::
   single: API authentication; accessing protected resources
 
Accessing protected resources
=============================
* **Supported methods:** GET, POST

The application uses the session token and its consumer key to access a 
protected resource.  The request needs to contain the following parameters and
to be signed using the consumer secret and session token secret:
 
 * oauth_consumer_key
 * oauth_request_method ('POST')
 * oauth_request_url (request URL)
 * oauth_signature_method ('HMAC-SHA1')
 * oauth_signature
 * oauth_token (session token)
 * oauth_timestamp (UNIX timestamp - seconds since Jan 1 1970)
    * this must be within 600 seconds of the current time.
 * oauth_nonce (random string)
 * oauth_version ('1.0')
  