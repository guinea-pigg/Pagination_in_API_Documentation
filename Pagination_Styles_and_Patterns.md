---
title: Pagination Styles and Patterns
layout: default
nav_order: 2
---

# 2. Pagination Styles and Patterns

Pagination is a crucial aspect of API documentation, especially when dealing with large datasets that need to be split into manageable pieces for retrieval. 

There are some common pagination styles, among which we can find: 
- Offset-based pagination,
- Cursor-based pagination,
- Keyset-based pagination,
- Page-based pagination.

**Offset-Based Pagination:**

Offset-based pagination is one of the most straightforward pagination styles. It involves specifying a numeric offset (typically the number of records to skip) and a limit (the number of records to fetch) in API requests. For example, if you have a list of items and you want to retrieve items 11-20, you would set the offset to 10 and the limit to 10.

However, offset-based pagination has its drawbacks. As the offset increases, the database needs to skip more records, which can lead to performance issues, especially with large datasets.

| Advantages                 | Disadvantages                                              |
|----------------------------|------------------------------------------------------------|
| Simple and easy to implement | Performance degrades with large datasets                   |
| Straightforward for developers | Increased server load due to skipping records               |
| Allows for precise navigation | Not suitable for real-time or frequently updated datasets   |
| Supports random access to pages | Limited scalability as dataset size grows                    |
|                              | Potential for inconsistent results if data changes during pagination |


