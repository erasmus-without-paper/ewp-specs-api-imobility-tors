Release notes
=============

This document describes all the changes made to the *Incoming Mobility
Transcripts of Records API* document, starting from its first beta draft
version.


0.7.0
-----

* The `modified_since` parameter of the `index` endpoint is now in the
  `xs:dateTime` format (not ISO 8601 format). See
  [this thread](https://github.com/erasmus-without-paper/general-issues/issues/27).

* `<index-url>` element was missing in `manifest-entry.xsd` (see
  [here](https://github.com/erasmus-without-paper/ewp-specs-api-imobility-tors/issues/5)).


0.6.0
-----

* New element in `manifest-entry.xsd`: `<sends-notifications/>`.


0.5.0
-----

* Renamed the document to *Incoming Mobility Transcript of Records API*.
  We decided that there is a big chance that the previous name (*Transcript of
  Records API*) might be used for a more general use case than the one provided
  by this API (i.e. exchanging Transcripts of Records which are not bounded to
  any mobilities).

  - Changed XML namespaces. All XML namespaces beginning with
    `https://github.com/erasmus-without-paper/ewp-specs-api-tors/`
    now begin with
    `https://github.com/erasmus-without-paper/ewp-specs-api-imobility-tors/`.

  - In the response, the root element `tors-get-response` was renamed to
    `imobility-tors-get-response`.

  - In `manifest-entry.xsd`, the `tors` element was renamed to
    `imobility-tors`.

* Some elements and parameters were renamed due to the recent changes in the
  Outgoing Mobilities API (see
  [here](https://github.com/erasmus-without-paper/ewp-specs-api-mobilities/issues/27)):

  - In the response, `mobility-id` element is now named `omobility-id`,
  - In the request, `mobility_id` parameters is now named `omobility_id`.
  - In `manifest-entry.xsd`, the `max-mobility-ids` element is now named
    `max-omobility-ids`.

* The `index` endpoint was added. Servers are REQUIRED to implement it (see
  [here](https://github.com/erasmus-without-paper/ewp-specs-mobility-flowcharts/issues/3)).


0.4.0
-----

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
  [here](https://github.com/erasmus-without-paper/ewp-specs-api-omobilities/issues/9#issuecomment-271272493).


0.1.0
-----

Initial release.
