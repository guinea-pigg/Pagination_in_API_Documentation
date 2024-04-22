---
title: Pagination Styles and Patterns
layout: default
nav_order: 3
---
# Pagination Styles and Patterns

Pagination is an aspect of API documentation that enables the user to retrieve big large datasets split into smaller pieces.

There are some common pagination styles, among which we can find: 
- [Offset-based pagination](#Offset-Based-Pagination),
- [Cursor-based pagination](#Cursor-Based-Pagination),
- [Keyset-based pagination](#Keyset-Based-Pagination),
- [Page-based pagination](#Page-Based-Pagination).

The user can divide large amount of data retrieved from an API by adding certain parameters to their query.

## Offset-Based Pagination <a id="Offset-Based-Pagination"></a>

Offset-based pagination is one of the most common pagination styles. It is used when a user wants to retrieve a specific number of records from an API.

Offset-based pagination involves specifying two additional parameters: 
- a **numeric offset** (typically the number of records to skip), and
- a **limit** (the number of records to fetch) in API requests.

If there is a list of items and the user wants to retrieve items 11-20, they would set the `offset` to 10 and the `limit` to 10.

An example of an API request to get offset-based paginated response:

`GET /api/resource?offset=0&limit=10`

Offset-based pagination has its drawbacks: as the offset increases, the database needs to skip more records. It can lead to performance issues, especially with large datasets.

| Advantages                 | Disadvantages                                              |
|----------------------------|------------------------------------------------------------|
| Simple and easy to implement | Performance degrades with large datasets                   |
| Straightforward for developers | Increased server load due to skipping records               |
| Allows for precise navigation | Not suitable for real-time or frequently updated datasets   |
| Supports random access to pages | Limited scalability as dataset size grows                    |
|                              | Potential for inconsistent results if data changes during pagination |

[Twitter API documentation](https://developer.twitter.com/en/docs/twitter-api/pagination) presents offset-based pagination as a method to return a specific number of records in one response.

## Cursor-Based Pagination <a id="Cursor-Based-Pagination"></a>

Cursor-based pagination in APIs works by using a **cursor**, which is a pointer indicating a specific position within a dataset. Instead of relying on numerical offsets like in offset-based pagination, cursor-based pagination uses cursors to keep track of the current position in the dataset.

Cursor-based pagination in API works in the following manner:

1. Initial Request: When the user makes the first request to retrieve data, they typically don't specify a cursor. The API returns the first page of results along with a cursor representing the end of the page.
2. Subsequent Requests: For subsequent requests to fetch additional pages of data, the user includes the cursor from the previous response in their request. This tells the API to start fetching data from where the previous page left off.
3. Pagination Flow: With each request, the API returns a new page of results along with a new cursor indicating the end of the current page. The user uses this cursor in the next request to fetch the next page of results.

Cursor-based pagination is commonly used when dealing with sorted datasets or when the underlying data can change frequently.

An example of an API request to get a cursor-based paginated response:

`GET /api/posts?limit=10&after=cursor123 HTTP/1.1`

In this example:

- Endpoint: `/api/posts` is the endpoint for retrieving a list of posts.
- Parameters:
  - `limit=10`: Specifies that we want to retrieve a maximum of 10 posts per page.
  - `after=cursor123`: Specifies the cursor that indicates the starting point for the next page of results. The value `cursor123` represents the cursor of the last item from the previous page.

| Advantages                                  | Disadvantages                                            |
|---------------------------------------------|----------------------------------------------------------|
| Improved performance with large datasets    | Requires support for cursor-based navigation on client side |
| Efficient for navigating sorted datasets   | Complexity in handling cursor values                     |
| Suitable for real-time or frequently updated datasets | Cursor values may become invalid if underlying data changes |
| Scalable and maintains consistent performance | Limited support in some database systems                  |
| Supports stable pagination across data changes |                                                        |

## Keyset-Based Pagination <a id="Keyset-Based-Pagination"></a>

Keyset-based pagination, also known as seek method pagination, is similar to cursor-based pagination but relies on unique, sortable keys instead of opaque cursors. This method is often preferred for datasets where natural ordering exists, such as timestamps or alphabetical order.

Keyset-based pagination offers predictable performance and is well-suited for large datasets, as it doesn't suffer from the performance issues associated with offset-based pagination.

| Advantages                                       | Disadvantages                                          |
|--------------------------------------------------|--------------------------------------------------------|
| Predictable performance                          | Requires a unique, sortable key in the dataset        |
| Efficient for large datasets                     | Complexity in handling multi-column ordering            |
| Well-suited for datasets with natural ordering   | Not suitable for unordered datasets                    |
| Avoids performance issues of offset-based pagination | Limited support in some database systems              |
| Stable pagination across data changes            |                                                        |

## Page-Based Pagination <a id="Page-Based-Pagination"></a>

Page-based pagination is perhaps the most user-friendly pagination style. Instead of dealing with offsets or cursors directly, users specify the page number and the number of items per page. For instance, requesting page 2 with 10 items per page would retrieve items 11-20.

While page-based pagination is intuitive for users, it may not be as efficient for large datasets, as it doesn't provide mechanisms for efficiently navigating to arbitrary points in the dataset.

| Advantages                                     | Disadvantages                                              |
|------------------------------------------------|------------------------------------------------------------|
| Intuitive and user-friendly                    | Inefficient for large datasets                             |
| Easy for users to understand and implement     | Lacks support for efficient navigation to arbitrary points |
| Simple implementation for developers           | May lead to inconsistent results if data changes           |
| Facilitates easy navigation through pages      | Limited scalability as dataset size grows                   |
|                                                | Potential for increased server load due to large page sizes |
