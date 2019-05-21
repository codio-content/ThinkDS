Most search engines can perform “boolean searches”, which means you can combine the results from multiple search terms using boolean logic. For example:



*  The search “java AND programming” might return only pages that contain both search terms: “java” and “programming”.
*  “java OR programming” might return pages that contain either term but not necessarily both.
*  “java -indonesia” might return pages that contain “java” and do not contain “indonesia”. 

Expressions like these that contain search terms and operators are called “queries”.


When applied to search results, the boolean operators `AND`, `OR`, and `-` correspond to the set operations `intersection`, `union`, and `difference`. For example, suppose



*  `s1` is the set of pages containing “java”,
*  `s2` is the set of pages containing “programming”, and
*  `s3` is the set of pages containing “indonesia”. 

In that case:



*  The intersection of `s1` and `s2` is the set of pages containing “java” AND “programming”.
*  The union of `s1` and `s2` is the set of pages containing “java” OR “programming”.
*  The difference of `s1` and `s2` is the set of pages containing “java” and not “indonesia”. 

In the next section you will write a method to implement these operations.