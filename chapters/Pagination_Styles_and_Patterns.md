---
title: Pagination Styles and Patterns
layout: default
nav_order: 3
---
# Pagination Styles and Patterns

Pagination is an aspect of API documentation that enables the user to retrieve big large datasets split into smaller pieces. The client (i.e. a person who uses an API) can divide large amount of data retrieved from an API by adding certain parameters to their query.

There are some common pagination styles, among which we can find: 
- [Offset-based pagination](#Offset-Based-Pagination),
- [Cursor-based pagination](#Cursor-Based-Pagination),
- [Keyset-based pagination](#Keyset-Based-Pagination),
- [Page-based pagination](#Page-Based-Pagination).

## Offset-Based Pagination <a id="Offset-Based-Pagination"></a>

Offset-based pagination is one of the most common pagination styles. It is used when a client wants to retrieve a specific number of records from an API.

Offset-based pagination involves specifying additional parameters: 
- a numeric `offset` (typically the number of records to skip), and
- a `limit` (the number of records to fetch) in API requests.

An example of an API request to get offset-based paginated response:

`GET /api/resource?offset=0&limit=10`

- Endpoint: `/api/resource` This endpoint specifies the resource that the client wants to access. It could be a resource such as a list of users, products, or posts.
- Parameters:
  - `offset=0`: Specifies that the client wants to start fetching records from the beginning of the dataset.
  - `limit=10`: Specifies that the client wants to retrieve a maximum of 10 records per page.


| Advantages                 | Disadvantages                                              |
|----------------------------|------------------------------------------------------------|
| Simple and easy to implement | Performance degrades with large datasets. Limited scalability as dataset size grows |
| Straightforward for developers | Increased server load due to skipping records               |
| Allows for precise navigation | Not suitable for real-time or frequently updated datasets. Potential for inconsistent results if data changes during pagination |
| Supports random access to pages |                     |

[Twitter API documentation](https://developer.twitter.com/en/docs/twitter-api/pagination) presents offset-based pagination.

## Cursor-Based Pagination <a id="Cursor-Based-Pagination"></a>

Cursor-based pagination in APIs works by using a cursor, which is a pointer indicating a specific position within a dataset. Instead of relying on numerical offsets like in offset-based pagination, cursor-based pagination uses cursors to keep track of the current position in the dataset.

Cursor-based pagination in API works in the following manner:

1. Initial Request: When the client makes the first request to retrieve data, they don't specify a cursor. The API returns the first page of results along with a cursor representing the end of the page.
2. Subsequent Requests: For subsequent requests to fetch additional pages of data, the client includes the cursor from the previous response in their request. This tells the API to start fetching data from where the previous page left off.
3. Pagination Flow: With each request, the API returns a new page of results along with a new cursor indicating the end of the current page. The client uses this cursor in the next request to fetch the next page of results.

Cursor-based pagination is commonly used when dealing with sorted datasets or when the data can change frequently.

An example of an API request to get a cursor-based paginated response:

`GET /api/posts?limit=10&after=cursor123 HTTP/1.1`

In this example:

- Endpoint: `/api/posts` is the endpoint for retrieving a list of posts.
- Parameters:
  - `limit=10`: Specifies that the client wants to retrieve a maximum of 10 posts per page.
  - `after=cursor123`: Specifies the cursor that indicates the starting point for the next page of results. The value `cursor123` represents the cursor of the last item from the previous page.

| Advantages                                  | Disadvantages                                            |
|---------------------------------------------|----------------------------------------------------------|
| Improved performance with large datasets. Scalable and maintains consistent performance | Requires support for cursor-based navigation on client side |
| Efficient for navigating sorted datasets   | Complexity in handling cursor values                     |
| Suitable for real-time or frequently updated datasets.  Supports stable pagination across data changes | Cursor values may become invalid if underlying data changes |
|  | Limited support in some database systems                  |

[GitHub REST API documentation](https://docs.github.com/en/rest?apiVersion=2022-11-28) presents cursor-based pagination.

## Keyset-Based Pagination <a id="Keyset-Based-Pagination"></a>

Keyset-based pagination uses unique, sortable keys. This method is often preferred for datasets where natural ordering exists, such as timestamps or alphabetical order.

Keyset-based pagination offers predictable performance and is well-suited for large datasets, as it doesn't suffer from the performance issues associated with offset-based pagination.

Keyset-based pagination involves specifying additional parameters:

- `limit`: Specifies the maximum number of items to return in the response. This parameter controls the page size or the number of items retrieved in each request.
- `starting_after`: Specifies the keyset indicating the starting point for fetching the next page of results. This keyset represents the identifier or value of the last item from the previous page.
- `ending_before`: Some APIs may use an `ending_before` parameter instead of a `starting_after` parameter. This parameter specifies the keyset indicating the ending point for fetching the previous page of results.

An example of an API request to get a keyset-based paginated response:

`GET /api/users?limit=10&starting_after=user123`

In this example:

- `limit=10` specifies the client wants to retrieve up to 10 users per page.
- `starting_after=user123` specifies the client wants to start fetching users after the user with the keyset `user123`.

As the result, the API would return a page of users starting after the user with the keyset `user123`.


| Advantages                                       | Disadvantages                                          |
|--------------------------------------------------|--------------------------------------------------------|
| Predictable performance. Avoids performance issues of offset-based pagination | Requires a unique, sortable key in the dataset        |
| Efficient for large datasets                     | Complexity in handling multi-column ordering            |
| Well-suited for datasets with natural ordering   | Not suitable for unordered datasets                    |
| Stable pagination across data changes | Limited support in some database systems              |

[Stripe API Reference documentation](https://docs.stripe.com/api) presents keyset-based pagination.

## Page-Based Pagination <a id="Page-Based-Pagination"></a>

Page-based pagination is a user-friendly pagination style. Instead of dealing with offsets or cursors directly, a client specifies the page number and the number of items per page. There typically aren't additional parameters specific to page-based pagination.

While page-based pagination is intuitive for clients, it may not be as efficient for large datasets, as it doesn't provide mechanisms for efficiently navigating to arbitrary points in the dataset.

An example of an API request to get a page-based paginated response:

`GET /api/posts?page=2&per_page=10`

In this example:

- Endpoint: `/api/posts` specifies the resource that the client wants to access. Tt could be a a list of posts, articles, or comments.
- Parameters:
  - `page=2`: Indicates that the clients wants to retrieve the second page of results.
  - `per_page=10`: Indicates that the clients wants to retrieve 10 records per page.

| Advantages                                     | Disadvantages                                              |
|------------------------------------------------|------------------------------------------------------------|
| Intuitive and user-friendly                    | Inefficient for large datasets. Limited scalability as dataset size grows |
| Simple implementation for developers | Lacks support for efficient navigation to arbitrary points |
| Facilitates easy navigation through pages | May lead to inconsistent results if data changes           |
|       | Potential for increased server load due to large page sizes |

[GitHub REST API documentation](https://docs.github.com/en/rest?apiVersion=2022-11-28) presents page-based pagination.

