---
title: Pagination Styles and Patterns
layout: default
nav_order: 2
---

# 2. Pagination Styles and Patterns

Pagination is a crucial aspect of API documentation, especially when dealing with large datasets that need to be split into manageable chunks for retrieval. Understanding different pagination styles and patterns is essential for creating efficient and user-friendly APIs. Here are the common pagination styles:

**Offset-Based Pagination:**

Offset-based pagination is one of the most straightforward pagination styles. It involves specifying a numeric offset (typically the number of records to skip) and a limit (the number of records to fetch) in API requests. For example, if you have a list of items and you want to retrieve items 11-20, you would set the offset to 10 and the limit to 10.

However, offset-based pagination has its drawbacks. As the offset increases, the database needs to skip more records, which can lead to performance issues, especially with large datasets.

**Cursor-Based Pagination:**

Cursor-based pagination addresses some of the performance issues associated with offset-based pagination. Instead of using numerical offsets, it uses opaque cursor values that point to specific items in the dataset. These cursors typically encode information about the position of the record, making it easier to navigate through pages efficiently.

Cursor-based pagination is commonly used when dealing with sorted datasets or when the underlying data can change frequently.

**Keyset-Based Pagination:**

Keyset-based pagination, also known as seek method pagination, is similar to cursor-based pagination but relies on unique, sortable keys instead of opaque cursors. This method is often preferred for datasets where natural ordering exists, such as timestamps or alphabetical order.

Keyset-based pagination offers predictable performance and is well-suited for large datasets, as it doesn't suffer from the performance issues associated with offset-based pagination.

**Page-Based Pagination:**

Page-based pagination is perhaps the most user-friendly pagination style. Instead of dealing with offsets or cursors directly, users specify the page number and the number of items per page. For instance, requesting page 2 with 10 items per page would retrieve items 11-20.

While page-based pagination is intuitive for users, it may not be as efficient for large datasets, as it doesn't provide mechanisms for efficiently navigating to arbitrary points in the dataset.

In summary, each pagination style has its advantages and drawbacks, and the choice of pagination style depends on factors such as the size and nature of the dataset, as well as the performance requirements of the API. By understanding these pagination styles and patterns, you can design APIs that provide efficient and seamless data retrieval experiences for users.
