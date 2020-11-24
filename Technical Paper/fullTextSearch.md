# Full-text search

Full-text search is a more advanced way to search a database. Full-text search quickly finds all instances of a term (word) in a table without having to scan rows and without having to know which column a term is stored in. Full-text search works by using text indexes. A text index stores positional information for all terms found in the columns you create the text index on. Using a text index can be faster than using a regular index to find rows containing a given value.

Full-text search capability in SQL Anywhere differs from searching using predicates such as LIKE, REGEXP, and SIMILAR TO, because the matching is term-based, not pattern-based.

String comparisons in full-text search use all the normal collation settings for the database. For example, if the database is configured to be case insensitive, then full-text searches will be case insensitive.

Except where noted, full-text search leverages all the international features supported by SQL Anywhere.

## Two ways to perform a full-text search

1. You can perform a full-text query either by using a CONTAINS clause in the FROM clause of a SELECT statement.

    SELECT *
    FROM MarketingInformation CONTAINS ( Description, 'cotton' );

2. By using a CONTAINS search condition (predicate) in a WHERE clause. Both return the same rows; however, use a CONTAINS clause in a FROM clause also returns scores for the matching rows.

    SELECT*
    FROM MarketingInformation
    WHERE CONTAINS ( Description, 'cotton' );

## When using external term breaker and prefilter libraries, there are several additional considerations

1. Querying and updating

    The external library must remain available for any operations that require updating, querying, or altering the text indexes built using the libraries.

2. Unloading and reloading

    The external library must be available during the unloading and reloading of data associated with the full-text index.

3. Database recovery

    The external library must be available to recover the database. This is because the database can not recover if there are operations in the transaction log that involved the external library since the last checkpoint.

### Practical Implementations of Full-text Search concept

1. Apache Lucene

    While suitable for any application that requires full-text indexing and searching capability, Lucene is recognized for its utility in the implementation of Internet search engines and local, single-site searching.

2. Apache Solr

    Solr (pronounced "solar") is an open-source enterprise-search platform, written in Java, from the Apache Lucene project. Its major features include full-text search, hit highlighting, faceted search, real-time indexing, dynamic clustering, database integration, NoSQL features, and rich document (e.g., Word, PDF) handling.

3. Elasticsearch

    Elasticsearch can be used to search for all kinds of documents. It provides scalable search, has a near real-time search, and supports multitenancy."Elasticsearch is distributed, which means that indices can be divided into shards and each shard can have zero or more replicas. Each node hosts one or more shards and acts as a coordinator to delegate operations to the correct shard(s). Rebalancing and routing are done automatically".Related data is often stored in the same index, which consists of one or more primary shards, and zero or more replica shards. Once an index has been created, the number of primary shards cannot be changed.

### References

1. <https://en.wikipedia.org/wiki/Apache_Lucene>
2. <https://en.wikipedia.org/wiki/Elasticsearc>
3. <https://en.wikipedia.org/wiki/Apache_Solr>
4. <https://en.wikipedia.org/wiki/Full-text_search>
5. <http://infocenter.sybase.com/help/index.jsp?topic=/com.sybase.help.sqlanywhere.12.0.1/dbusage/full-text-search-what-is-it.html>
