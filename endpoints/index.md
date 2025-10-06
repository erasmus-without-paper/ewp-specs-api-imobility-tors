Incoming Mobility ToRs Index endpoint
=====================================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This endpoint allows the sending institution to access a list of all mobility
IDs for which the receiving institution has already attached corresponding
Transcripts of Records, and which the caller can read (via the `get` endpoint).


Request method
--------------

 * Requests MUST be made with either HTTP GET or HTTP POST method. Servers MUST
   support both these methods. Servers SHOULD reject all other request methods.

 * Clients are advised to use POST when passing large number of parameters
   (servers MAY set a limit on their GET query string length).


Request parameters
------------------

Parameters MUST be provided in the regular `application/x-www-form-urlencoded`
format.



### `modified_since` (optional)

A datetime string in the [`xs:dateTime` format][xs-datetime], e.g.
`2004-02-12T15:19:21+01:00`.

If given, then the server SHOULD filter the returned transcripts of records
to the ones which have been either created or modified after the given point in
time.

 * Servers MAY include transcripts which were *not* modified. For example, if
   the server only *suspects* that the transcript has been modified, then it is
   okay to include its corresponding mobility's ID in the response.

 * As we previously explained [here][index-pulling], clients MAY use the
   `index` and `get` endpoints as a pull-based method of synchronization,
   complementary to CNRs. It is RECOMMENDED for the
   servers to support this parameter, to avoid unnecessary network traffic.


Permissions
-----------

Only selected Transcripts of Records should be accessible to the caller.
Visibility of objects SHOULD be kept in sync with the visibility described in
the `get` endpoint. That is:

 * Servers MUST publish all mobility IDs corresponding to every Transcript of
   Record which is otherwise accessible (to the same caller) via the `get`
   endpoint.

 * Server MUST NOT publish IDs of objects which would NOT be accessible (to the
   same caller) via its `get` endpoint. Clients which receive certain mobility
   IDs from the `index` endpoint should be able to fetch (via the `get`
   endpoint) all Transcripts of Records which correspond with these mobility
   IDs.


Response
--------

Servers MUST respond with a valid XML document described by the
[index-response.xsd](index-response.xsd) schema. See the schema annotations
for further information.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[registry-spec]: https://github.com/erasmus-without-paper/ewp-specs-api-registry
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
[institutions-api]: https://github.com/erasmus-without-paper/ewp-specs-api-institutions
[index-pulling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#index-pulling
[xs-datetime]: https://www.w3.org/TR/xmlschema11-2/#dateTime
