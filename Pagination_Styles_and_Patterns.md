---
title: Pagination Styles and Patterns
layout: default
nav_order: 3
---

# Pagination Styles and Patterns

Pagination is a crucial aspect of API documentation, especially when dealing with large datasets that need to be split into manageable pieces for retrieval. 

There are some common pagination styles, among which we can find: 
- Offset-based pagination,
- Cursor-based pagination,
- Keyset-based pagination,
- Page-based pagination.

## Offset-Based Pagination:

Offset-based pagination is one of the most straightforward pagination styles. It involves specifying a numeric offset (typically the number of records to skip) and a limit (the number of records to fetch) in API requests. For example, if you have a list of items and you want to retrieve items 11-20, you would set the offset to 10 and the limit to 10.

However, offset-based pagination has its drawbacks. As the offset increases, the database needs to skip more records, which can lead to performance issues, especially with large datasets.

| Advantages                 | Disadvantages                                              |
|----------------------------|------------------------------------------------------------|
| Simple and easy to implement | Performance degrades with large datasets                   |
| Straightforward for developers | Increased server load due to skipping records               |
| Allows for precise navigation | Not suitable for real-time or frequently updated datasets   |
| Supports random access to pages | Limited scalability as dataset size grows                    |
|                              | Potential for inconsistent results if data changes during pagination |

## Cursor-Based Pagination:

Cursor-based pagination addresses some of the performance issues associated with offset-based pagination. Instead of using numerical offsets, it uses opaque cursor values that point to specific items in the dataset. These cursors typically encode information about the position of the record, making it easier to navigate through pages efficiently.

Cursor-based pagination is commonly used when dealing with sorted datasets or when the underlying data can change frequently.

| Advantages                                  | Disadvantages                                            |
|---------------------------------------------|----------------------------------------------------------|
| Improved performance with large datasets    | Requires support for cursor-based navigation on client side |
| Efficient for navigating sorted datasets   | Complexity in handling cursor values                     |
| Suitable for real-time or frequently updated datasets | Cursor values may become invalid if underlying data changes |
| Scalable and maintains consistent performance | Limited support in some database systems                  |
| Supports stable pagination across data changes |                                                        |

## Keyset-Based Pagination:

Keyset-based pagination, also known as seek method pagination, is similar to cursor-based pagination but relies on unique, sortable keys instead of opaque cursors. This method is often preferred for datasets where natural ordering exists, such as timestamps or alphabetical order.

Keyset-based pagination offers predictable performance and is well-suited for large datasets, as it doesn't suffer from the performance issues associated with offset-based pagination.

| Advantages                                       | Disadvantages                                          |
|--------------------------------------------------|--------------------------------------------------------|
| Predictable performance                          | Requires a unique, sortable key in the dataset        |
| Efficient for large datasets                     | Complexity in handling multi-column ordering            |
| Well-suited for datasets with natural ordering   | Not suitable for unordered datasets                    |
| Avoids performance issues of offset-based pagination | Limited support in some database systems              |
| Stable pagination across data changes            |                                                        |

## Page-Based Pagination:

Page-based pagination is perhaps the most user-friendly pagination style. Instead of dealing with offsets or cursors directly, users specify the page number and the number of items per page. For instance, requesting page 2 with 10 items per page would retrieve items 11-20.

While page-based pagination is intuitive for users, it may not be as efficient for large datasets, as it doesn't provide mechanisms for efficiently navigating to arbitrary points in the dataset.

| Advantages                                     | Disadvantages                                              |
|------------------------------------------------|------------------------------------------------------------|
| Intuitive and user-friendly                    | Inefficient for large datasets                             |
| Easy for users to understand and implement     | Lacks support for efficient navigation to arbitrary points |
| Simple implementation for developers           | May lead to inconsistent results if data changes           |
| Facilitates easy navigation through pages      | Limited scalability as dataset size grows                   |
|                                                | Potential for increased server load due to large page sizes |
