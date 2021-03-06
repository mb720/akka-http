# withRangeSupport

## Description

Transforms the response from its inner route into a `206 Partial Content`
response if the client requested only part of the resource with a `Range` header.

Augments responses to `GET` requests with an `Accept-Ranges: bytes` header and converts them into partial responses
if the request contains a valid `Range` request header. The requested byte-ranges are coalesced (merged) if they
lie closer together than the specified `rangeCoalescingThreshold` argument.

In order to prevent the server from becoming overloaded with trying to prepare `multipart/byteranges` responses for
high numbers of potentially very small ranges the directive rejects requests requesting more than `rangeCountLimit`
ranges with a `TooManyRangesRejection`.
Requests with unsatisfiable ranges are rejected with an `UnsatisfiableRangeRejection`.

The `withRangeSupport()` form (without parameters) uses the `range-coalescing-threshold` and `range-count-limit`
settings from the `akka.http.routing` configuration.

This directive is transparent to non-`GET` requests.

See also: [RFC 7233](https://tools.ietf.org/html/rfc7233)

## Example

@@snip [RangeDirectivesExamplesTest.java](../../../../../../../test/java/docs/http/javadsl/server/directives/RangeDirectivesExamplesTest.java) { #withRangeSupport }