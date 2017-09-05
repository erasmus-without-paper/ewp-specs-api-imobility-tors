Release notes
=============

This document describes all the changes made to the *Transcripts of Records
API* document, starting from its first beta draft version.


Master (unreleased)
-------------------

Many backward-incompatible changes.

* `manifest-entry.xsd`: The `<url>` element has been renamed to `<get-url>`.

* Parts of the existing documentation have been moved to a separate page
  (which now describes the `get` endpoint).

* The `get` endpoint response was renamed and moved to other XML namespace.

  Previously, the root element of the `get` endpoint's response was:

  ```xml
  <tors-response xmlns="https://github.com/erasmus-without-paper/ewp-specs-api-tors/tree/stable-v1"/>
  ```

  And now it is:

  ```xml
  <tors-get-response xmlns="https://github.com/erasmus-without-paper/ewp-specs-api-tors/blob/stable-v1/endpoints/get-response.xsd"/>
  ```

  Note, that **both** namespace *and* the element's name has changed.


0.3.0
-----

 * This API now requires implementers to upgrade their implementations to
   [Version 2](https://github.com/erasmus-without-paper/ewp-specs-sec-intro/tree/stable-v2)
   of the *Authentication and Security* document.

   In particular, this means that the clients MUST be aware of the fact, that
   the server is no longer required to support methods of authentication and
   encryption which it *was* required to support in the previous versions of
   this API. Clients SHOULD consult the newly introduced `<http-security>`
   element in the server's manifest entry before making their requests.


0.2.1
-----

* Explicitly declare that this version still requires the use of
  [Version 1](https://github.com/erasmus-without-paper/ewp-specs-sec-intro/tree/stable-v1)
  of the *Authentication and Security* document. You can find more information
  on the planned process of updating security requirements
  [here](https://github.com/erasmus-without-paper/ewp-specs-sec-intro/issues/1).


0.2.0
-----

* Changed XML namespaces (as part of
  [this issue](https://github.com/erasmus-without-paper/ewp-specs-api-iias/issues/22)).
  Since this version, this API is in the `stable-v1` XML namespace.

  This does not mean that this API is stable. It can still change in
  backward-incompatible ways, until version `1.0.0` is released.


0.1.2
-----

* Mobility IDs are now of `ewp:AsciiPrintableIdentifier` type
  ([why?](https://github.com/erasmus-without-paper/general-issues/issues/23)).

* `minOccurs` and `maxOccurs` are now provided explicitly
  ([why?](https://github.com/erasmus-without-paper/general-issues/issues/22)).


0.1.1
-----

* Modified the examples so that the use proper surrogate IDs, as discussed
  [here](https://github.com/erasmus-without-paper/ewp-specs-api-mobilities/issues/9#issuecomment-271272493).


0.1.0
-----

Initial release.
