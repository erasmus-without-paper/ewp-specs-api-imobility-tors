Incoming Mobility ToRs Get endpoint
===================================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This endpoint allows the client (usually the sending HEI) to retrieve
Transcripts of Records for specific Incoming Mobilities from the receiving HEI.


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



### `omobility_id` (repeatable, required)

A list of Outgoing Mobility identifiers (max `<max-omobility-ids>` items) - IDs
of Outgoing Mobility objects for which the client wants to retrieve
corresponding Transcripts of Records. The HEI covered by the caller
MUST be the sending partner of all these
mobilities (unmatched mobilities will be ignored).

This parameter is *repeatable*, so the request MAY contain multiple occurrences
of it. The server is REQUIRED to process all of them.

Server implementers provide their own chosen value of `<max-omobility-ids>` via
their manifest entry (see [manifest-entry.xsd](../manifest-entry.xsd)). Clients
SHOULD parse this value (or assume it's equal to `1`).


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * Invalid (unknown) `omobility_id` values MUST be **ignored**. Servers MUST
   return a valid (HTTP 200) XML response in such cases, but the response will
   simply not contain the information on the unknown `omobility_id` values. If
   all values are unknown, servers MUST respond with an empty `<response>`
   element. This requirement is true even when `<max-omobility-ids>` is `1`.

 * If the caller doesn't have permission to view some of the ToRs corresponding
   to provided `omobility_ids`, then such `omobility_ids` MUST also be ignored,
   exactly as above. Servers MUST return a valid (HTTP 200) XML response in
   such cases.

 * Currently, clients have no way of telling the difference between "this
   `omobility_id` does not exist" and "it does exist, but you don't have access
   to it". In both cases, the proper `<tor>` element will simply be missing
   from the response.

 * If the length of `omobility_id` list is greater than `<max-omobility-ids>`,
   then servers SHOULD respond with HTTP 400. Clients SHOULD split large
   requests into a couple of smaller ones (based on the `<max-omobility-ids>`
   value obtained from the Registry).


Response
--------

Servers MUST respond with a valid XML document described by the
[get-response.xsd](get-response.xsd) schema. See the schema annotations for
further information.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[omobilities-api]: https://github.com/erasmus-without-paper/ewp-specs-api-omobilities
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
