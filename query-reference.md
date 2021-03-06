---

copyright:
  years: 2019, 2021
lastupdated: "2021-04-13"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Query reference
{: #query-reference}

The full list of {{site.data.keyword.discoveryshort}} query parameters, operators, and aggregations. These are used when writing queries with the {{site.data.keyword.discoveryshort}} Query Language. For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}. For an overview of query concepts, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
{: shortdesc}

In the {{site.data.keyword.discoveryshort}} tooling, you can write and test [natural language queries](/docs/discovery-data?topic=discovery-data-query-parameters#nlq) on the *Improve and customize* page.
{: tip}

## Parameters descriptions
{: #parameter-descriptions}

Query parameters enable you to search your collection, identify a result set, and perform analysis on result sets.


| Parameter | Description | Example |
|:-------------------|------------------------------------------------------------|--------------------------------|
| **Search parameters** |  |  |
| [query](/docs/discovery-data?topic=discovery-data-query-parameters#query) | A ranked query language search for matching documents. | `query=bees` |
| [filter](/docs/discovery-data?topic=discovery-data-query-parameters#filter) | An unranked query language search for matching documents. | `filter=bees` |
| [natural_language_query](/docs/discovery-data?topic=discovery-data-query-parameters#nlq) | A ranked natural language search for matching documents | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/discovery-data?topic=discovery-data-query-parameters#aggregation) | A statistical query of the results set | `aggregation=term(enriched_text.entities.type)` |
| **Structure parameters** | | |
| [count](/docs/discovery-data?topic=discovery-data-query-parameters#count) | The number of `result` documents to return. | `count=15` |
| [offset](/docs/discovery-data?topic=discovery-data-query-parameters#offset) | The number of results to ignore before returning `result` documents from the results set | `offset=100` |
| [return](/docs/discovery-data?topic=discovery-data-query-parameters#return) | List of fields to return | `return=title,url` |
| [sort](/docs/discovery-data?topic=discovery-data-query-parameters#sort) | Field to sort results set by | `sort=enriched_text.sentiment.document.score` |
| [highlight](/docs/discovery-data?topic=discovery-data-query-parameters#highlight) | Highlight query matches | `highlight=true` |
| [spelling suggestions](/docs/discovery-data?topic=discovery-data-query-parameters#spell) | Spelling suggestions returned for natural language queries | `spelling_suggestions=true` |

### Query limitations
{: #query-limitations}

You cannot query on field names that contain the following:
- Numerical characters (`0 - 9`) in the suffix of the field name (for example `extracted-content2`).
- The characters `_`, `+`, and `-` in the prefix of the `field_name` (for example `+extracted-content`).
- The characters `.`, `,`, and `:` in the `field_name` (for example `new:extracted-content`)

## Operators
{: #operators}

Operators are the separators between different parts of a query. Available operators:

| Operator | Description | Example |
|:-------------------|------------------------------------------------------------|--------------------------------|
| [.](/docs/discovery-data?topic=discovery-data-query-operators#delimiter) | JSON delimiter | `enriched_text.concepts.text` |
| [:](/docs/discovery-data?topic=discovery-data-query-operators#includes) | Includes | `text:computer` |
| [::](/docs/discovery-data?topic=discovery-data-query-operators#match) | Exact match | `title::"Query building"` |
| [:!](/docs/discovery-data?topic=discovery-data-query-operators#notinclude) | Does not include | `text:!computer` |
| [::!](/docs/discovery-data?topic=discovery-data-query-operators#notamatch) | Not an exact match | `text::!winter` |
| [\\](/docs/discovery-data?topic=discovery-data-query-operators#escape) | Escape character | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/discovery-data?topic=discovery-data-query-operators#phrase) | Phrase query | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/discovery-data?topic=discovery-data-query-operators#nestedquery) | Nested grouping | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/discovery-data?topic=discovery-data-query-operators#or) | or | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/discovery-data?topic=discovery-data-query-operators#and) | and | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/discovery-data?topic=discovery-data-query-operators#comparisons) | Numerical comparisons |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/discovery-data?topic=discovery-data-query-operators#multiplier) | Score multiplier | `text:IBM^3` |
| [*](/docs/discovery-data?topic=discovery-data-query-operators#wildcard) | Wildcard | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/discovery-data?topic=discovery-data-query-operators#variation) | String variation | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/discovery-data?topic=discovery-data-query-operators#exists) | Exists | `title:*` |
| [!*](/docs/discovery-data?topic=discovery-data-query-operators#dnexist) | Does not exist | `title!*` |

## Aggregations
{: #aggregations}

Aggregations return a set of data values. Available aggregations:

| Aggregation | Description | Example |
|:-------------------|------------------------------------------------------------|--------------------------------|
| [term](/docs/discovery-data?topic=discovery-data-query-aggregations#term) | Count of identical values | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/discovery-data?topic=discovery-data-query-aggregations#aggfilter) | Filter results set to defined pattern | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/discovery-data?topic=discovery-data-query-aggregations#nested) | Restrict aggregation | `nested(enriched_text.entities)` |
| [histogram](/docs/discovery-data?topic=discovery-data-query-aggregations#histogram) | Interval based distribution | `histogram(product.price,interval:1)` |
| [timeslice](/docs/discovery-data?topic=discovery-data-query-aggregations#timeslice) | Time base distribution | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/discovery-data?topic=discovery-data-query-aggregations#top_hits) | Top ranked results documents for the current aggregation | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/discovery-data?topic=discovery-data-query-aggregations#unique_count) | Count of unique values for a field within an aggregation | `unique_count(enriched_text.entities.type)` |
| [max](/docs/discovery-data?topic=discovery-data-query-aggregations#max) | Maximum value for the specified field in the results set. | `max(product.price)` |
| [min](/docs/discovery-data?topic=discovery-data-query-aggregations#min) | Minimum value for the specified field in the results set. | `min(product.price)` |
| [average](/docs/discovery-data?topic=discovery-data-query-aggregations#average) |Mean value for the specified field in the results set. | `average(product.price)` |
| [sum](/docs/discovery-data?topic=discovery-data-query-aggregations#sum) | Sum of all fields in the results set. | `sum(product.price)` |
