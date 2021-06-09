---
description: Paging through results in the Boardroom API
---

# Pagination

For all API routes that return a list of data, the Boardroom API follows a standardized approach to pagination when returning a subset of all available results.

{% hint style="info" %}
See all available HTTP routes, query parameters, and example responses in the [API Reference](api-reference.md)
{% endhint %}

### Overview

Pagination is handled via the following two parameters:

* `limit` - **If providing a limit, then the API will only return at most this many results.** Depending on the route, there may be a maximum limit that is enforced. If providing a value for `limit` greater than the max, or for other internal reasons to the platform, you may not always get back as many items as requested with this parameter.
* `cursor` - **If providing a cursor, then the API will resume the paginated query from a previous position**. If a paginated response has more items than were returned, a `nextCursor` value is provided in the response. Passing this value back to the endpoint for a subsequent request will continue paging through the result set. The cursor should be treated as an arbitrary opaque string.

### Example

The **List Proposals** route in the [Boardroom API](api-reference.md) is a paginated route.  If we make the following request:

```text
GET https://api.boardroom.info/v1/proposals?limit=5
```

Then the following response is returned:

```javascript
{
  "data": [
    {
      "refId": "cHJvcG9zYWw6aW5kZXhjb29wOmRlZmF1bHQ6cW1iZ2o1cDlvanp3am95Ymtha2hhemQ1ZWxtZXhuNHpramFlNnZ2aXU5a3Vqbg==",
      "id": "QmbGj5P9oJZWjoybkaKhAZD5ELmexN4zKJAe6VViu9kUJN",
      "title": "Decision Gate 2: Bankless BED Index",
      // ... more fields
    },
    {
      "refId": "cHJvcG9zYWw6aW5kZXhlZDpkZWZhdWx0OjEz",
      "id": "13",
      "title": "Add BNT as a candidate asset to CC10 ",
      // ... more fields
    },
    // ... more items
  ],
  "nextCursor": "eyJyZWZJZCI6ImNISnZjRzl6WVd3NmFXUnNaV1pwYm1GdVkyVTZjMjVoY0hOb2IzUTZjVzE1ZVRscWNtbHRjbXg0YUdwcE1tNXFiWEZ6Wldsc2NtNTFkWGxxYlhkd2RHRjBaM041ZG5RMWMybDFhZz09Iiwic3RhcnRUaW1lc3RhbXAiOjE2MjMxOTY4MDB9"
}
```

Since a `nextCursor` value was provided, there are more items to this response. To get the next page, we use the `nextCursor` value from the response in the subsequent request as the `cursor` parameter:

```text
GET https://api.boardroom.info/v1/proposals?limit=5&cursor=eyJyZWZJZ...
```

{% hint style="info" %}
If `nextCursor` is returned, there are more pages. If it's missing in the response, there are no more pages in the list.
{% endhint %}

