---
title: API Documentation Standards and Guidelines
layout: default
nav_order: 6
---

# API Documentation Standards and Guidelines

Pagination is a crucial aspect of API documentation, and documenting it effectively is essential for users to understand how to retrieve and navigate through paginated data. Standards and guidelines for documenting pagination in API reference documentation cover areas such as:
   - [documenting pagination in API reference](#Documenting-Pagination-in-API-reference),
   - [providing usage examples](#Providing-Usage-Examples),
   - [writing clear pagination instructions](#Writing-Clear-Pagination-Instructions).

It is worth noting that numerous API documentations have general introductions with limited space for the pagination concept. The content described in documentation heavily depends on the API's structure and logic. Pagination is usually just a small part of the overall API documentation introduction. In case of API that handles small loads of data, pagination is frequently not applied.

<a id="Documenting-Pagination-in-API-reference"></a>
## Documenting Pagination in API Reference

### 1. Introduction to Pagination 

Documentation has to provide an overview of pagination and its importance in retrieving large datasets efficiently.

A chapter on pagination in API is available at the [X Developer Platform](https://developer.x.com/en/docs/twitter-api/pagination). The chapter includes:
- use cases for pagination,
- pagination token definitions,
- fundamentals of pagination,
- pagination examples.

The chapter covers all aspects of managing pagination for developers using X's API, beginning from short explanation what pagination is. 
<a id="Pagination-Parameters"></a>
### 2. Pagination Parameters

Documentation should describe the pagination parameters supported by the API. Depending on a type of pagination, it can include:
   - `page`: specifying the page number to retrieve,
   - `limit`: specifying the maximum number of items per page,
   - additionally: any other parameters specific to the pagination style used, such as cursor values or keyset identifiers.

An example showing this practice is documentation at the [X Developer Platform](https://developer.x.com/en/docs/twitter-api/pagination). It lists different parameters that facilitate the use of pagination in the documentation, such as: `next_token`, `previous_token`, `max_results`, `pagination_token`. In X's API `pagination_token` is a different name for `offset`, making it a typical example of offset-based API. 

To know more about offset-based API, go to chapter titled [Pagination Styles and Patterns](Pagination_Styles_and_Patterns.md).
<a id="Request-Structure"></a>
### 3. Request Structure

Documentation should clearly outline the structure of the API request when paginating data. It can include elements such as:
   - parameters for specifying the page number or cursor,
   - the number of records to be returned per page (page size),
   - any additional filters or sorting options that can be applied to the request.

Documentation at the [X Developer Platform](https://developer.x.com/en/docs/twitter-api/pagination) shows an exemplary request and the sequence of further requests that retrieves the next pages of data. 

The initial request specifies a user ID (`2244994945`) and the time period for obtaining the results, from January 1, 2019, at 17:00:00 UTC to December 12, 2019, at 00:00:00 UTC.

`https://api.twitter.com/2/users/2244994945/tweets?tweet.fields=created_at&max_results=100&start_time=2019-01-01T17:00:00Z&end_time=2020-12-12T01:00:00Z`

Because the API parameter `max_results` is set to 100 and there are approximately 295 posts created by user ID `2244994945`, the results are spread across more than one page. According to the explanation found in the API documentation, to get the second page of results, the request needs the following parameters:

- `max_results=100`
- `tweet.fields=created_at`
- `start_time=2019-01-01T17:00:00Z`
- `end_time=2020-12-12T01:00:00Z`
- `pagination_token=7140w`

Documentation highlights that in order "to get the next page, take the `next_token value` directly from the response (`7140w`) and set it as the `pagination_token` for the next request call."
<a id="Response-Structure"></a>
### 4. Response Structure

Documentation should describe the structure of the API response when paginating data. It can include elements such as:
   - total number of records available,
   - links or cursors for navigating to the next or previous pages,
   - representation of the current page of data.

Documentation at the [X Developer Platform](https://developer.x.com/en/docs/twitter-api/pagination) shows an exemplary response:

`{
  "data": [
    {
      "created_at": "2020-12-11T20:44:52.000Z",
      "id": "1337498609819021312",
      "text": "Thanks to everyone who tuned in today..."
    },
    .
    .
    .
   {
      "created_at": "2020-05-06T17:24:31.000Z",
      "id": "1258085245091368960",
      "text": "It’s now easier to understand Tweet impact..."
    }
  ],
  "meta": {
    "oldest_id": "1258085245091368960",
    "newest_id": "1337498609819021312",
    "result_count": 100,
    "next_token": "7140w"
  }
}`

What's interesting, X's documentation on API doesn't explain each part of the response. 

A part of the response called `data` contains an array of posts. Each post has:
  - `created_at`: explaining when the post was made,
  - `id`: a unique identifier for the post,
  - `text`: the content of the post.

A part of the response called `meta` provides extra information about the data:
  - `oldest_id`: the ID of the oldest post in this set,
  - `newest_id`: the ID of the newest post in this set,
  - `result_count`: the number of posts in this response (100),
  - `next_token`: a token to get the next set of results.

### 5. Error Handling

Documentation can list any potential errors or edge cases related to pagination, such as invalid pagination parameters or reaching the end of the dataset. In practice, chapters dedicated to pagination in APIs rarely cover error handling specific to pagination. This topic is usually addressed in general troubleshooting sections.

<a id="Providing-Usage-Examples"></a>
## Providing Usage Examples

### 1. Basic Examples

The documentation should include simple examples demonstrating how to paginate through data using the API. It should show how to retrieve the first page, navigate to the next page, and adjust pagination parameters.

Documentation at the [X Developer Platform](https://developer.x.com/en/docs/twitter-api/pagination) shows simple examples on [pagination parameters](#Pagination-Parameters), [request structure](#Request-Structure), or [response structure](#Response-Structure). 

### 2. Advanced Examples

The documentation should show more complex examples that explain different pagination scenarios, such as sorting, filtering, or combining pagination with other query parameters.

Documentation on [YouTube API](https://developers.google.com/youtube/v3/guides/implementation/pagination?hl=en) explains how to retrieve additional sets of results for YouTube Data API queries, explaining additional parameters (e.g. `nextPageToken`, `prevPageToken`), and giving exemplary queries.

### 3. Sample Code Snippets

The documentation should show code snippets in various programming languages illustrating how to integrate pagination into API requests. It should also include comments to explain each step and highlight key pagination parameters. 

In practice, code snippets are most often shown in a separate chapter that is not dedicated exclusively to pagination but generic use of API. Here an example can be documentation on [YouTube API](https://developers.google.com/youtube/v3/code_samples/code_snippets).

<a id="Writing-Clear-Pagination-Instructions"></a>
## Writing Clear Pagination Instructions

### 1. Define Usage Patterns

Documentation should explain how users should format API requests to paginate data effectively. It should provide examples of valid pagination requests using the supported parameters.

[Stripe API](https://docs.stripe.com/api/pagination) documentation includes a separate chapter on pagination, explaining how to use cursor-based pagination with specific parameters (`starting_after` and `ending_before`). It also provides a sample response in a window next to the explanation.

### 2. Clarify Default Behavior

If the API has default pagination settings or behaviors, documentation should explain them explicitly. Users should understand what happens if they don't specify pagination parameters in their requests.

[Example from Mailchimp API]():LINK !!

### 3. Address Edge Cases

The documentation should anticipate common questions or confusion points related to pagination, such as navigating to specific pages or handling large datasets. Provide detailed instructions or troubleshooting tips to address these scenarios.

[Example from Google Books API](https://developers.google.com/books/docs/v1/using):

`To navigate to a specific page, include the startIndex parameter in your request. If the specified index exceeds the total number of items, the API will return an empty list.`
