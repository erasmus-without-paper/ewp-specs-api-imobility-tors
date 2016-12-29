Transcripts of Records API
==========================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Transcripts of Records API**. This API is
implemented by the receiving institution. It allows the receiving institution
to retrieve Transcripts of Records for a given set of mobility IDs.


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


### `receiving_hei_id` (required)

SCHAC ID of the institution which is (or was) the receiving partner of all the
mobilities provided in `mobility_id` parameter list. This parameter MUST be
required by the server even if the server covers only a single institution.


### `mobility_id` (repeatable, required)

A list of Outgoing Mobility identifiers (max `<max-mobility-ids>` items) - IDs
of Outgoing Mobility objects for which the client wants to retrieve
corresponding Transcripts of Records. The HEI referenced in the
`receiving_hei_id` parameter must be the receiving partner of all these
mobilities (unmatched mobilities will be ignored).

This parameter is *repeatable*, so the request MAY contain multiple occurrences
of it. The server is REQUIRED to process all of them.

Server implementers provide their own chosen value of `<max-mobility-ids>` via
their manifest entry (see [manifest-entry.xsd](manifest-entry.xsd)). Clients
SHOULD parse this value (or assume it's equal to `1`).


Permissions
-----------

All requests from the EWP Network MUST be allowed access to this API. Consult
the [Echo API][echo] specs for details on handling unprivileged requests.

However, only selected Transcripts of Records should be accessible to the
caller:

 * If a ToR has not been approved yet, then it SHOULD NOT be accessible via
   this API. Once ToR is approved, the receiving HEI SHOULD request its
   recognition (via sending HEI's [Outgoing Mobilities API](mobilities-api)).

 * If the caller covers the sending HEI of the given mobility, then he MUST be
   allowed read access to the mobility's corresponding ToR.

 * If the caller covers the receiving HEI (yourself) of the given mobility,
   then he MAY be allowed read access to the mobility's corresponding ToR. (It
   seems reasonable to do so, but we leave this decision to your team.)

 * All other callers SHOULD NOT be allowed to view the ToR.

 * Note, that servers will need to verify these access rights for each ID on
   the `mobility_id` list. It is possible that the caller has access to only
   some of the mobilities. (If this seems problematic, then you can always
   simply set your `<max-mobility-ids>` to `1`.)


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * Invalid (unknown) `mobility_id` values MUST be **ignored**. Servers MUST
   return a valid (HTTP 200) XML response in such cases, but the response will
   simply not contain the information on the unknown `mobility_id` values. If
   all values are unknown, servers MUST respond with an empty `<response>`
   element. This requirement is true even when `<max-mobility-ids>` is `1`.

 * If the caller doesn't have permission to view some of the ToRs corresponding
   to provided `mobility_ids`, then such `mobility_ids` MUST also be ignored,
   exactly as above. Servers MUST return a valid (HTTP 200) XML response in
   such cases.

 * Currently, clients have no way of telling the difference between "this
   `mobility_id` does not exist" and "it does exist, but you don't have access
   to it". In both cases, the proper `<tor>` element will simply be missing
   from the response.

 * If the length of `mobility_id` list is greater than `<max-mobility-ids>`,
   then servers SHOULD respond with HTTP 400. Clients SHOULD split large
   requests into a couple of smaller ones (based on the `<max-mobility-ids>`
   value obtained from the Registry).


Response
--------

Servers MUST respond with a valid XML document described by the [response.xsd]
(response.xsd) schema. See the schema annotations for further information.


Data model entities involved in the response
--------------------------------------------

 * Mobility
 * Learning Agreement
 * Learning Agreement Component
 * Learning Opportunity Specification
 * Learning Opportunity Instance
 * Result Distribution
 * Academic Term


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[registry-spec]: https://github.com/erasmus-without-paper/ewp-specs-api-registry
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
[institutions-api]: https://github.com/erasmus-without-paper/ewp-specs-api-institutions
[mobilities-api]: https://github.com/erasmus-without-paper/ewp-specs-api-mobilities
