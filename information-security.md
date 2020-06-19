---

copyright:
  years: 2020
lastupdated: "2020-06-12"

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

# Information security 
{: #information-security}

![IBM Cloud only](images/cloudonly.png)</br>
IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions.
{: shortdesc}

**Notice:**
Clients are responsible for ensuring their own compliance with various laws and regulations, including the European Union General Data Protection Regulation. Clients are solely responsible for obtaining advice of competent legal counsel as to the identification and interpretation of any relevant laws and regulations that may affect the clients' business and any actions the clients may need to take to comply with such laws and regulations.

The products, services, and other capabilities described herein are not suitable for all client situations and might have restricted availability. IBM does not provide legal, accounting, or auditing advice or represent or warrant that its services or products ensure that clients are in compliance with any law or regulation.

If you need to request GDPR support for {{site.data.keyword.cloud}} {{site.data.keyword.watson}} resources that are created, see [GDPR Subject Access Request](/docs/watson?topic=watson-gdpr-sar).

## European Union General Data Protection Regulation (GDPR)
{: #gdpr}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions to assist them on their journey to GDPR compliance.

Learn more about IBM's own GDPR readiness journey and our GDPR capabilities and offerings to support your compliance journey [here](https://www.ibm.com/data-responsibility/gdpr/){: external}.

## Labeling and deleting data in {{site.data.keyword.discoveryshort}}
{: #gdpr-discovery}

{{site.data.keyword.discoveryshort}} includes an API to label data per call.

With this API you can:

- Label your data with a customer ID.
- Delete all data for a specific customer ID, including related notices.

Data is labeled by adding a `customer_id` of your choice (see restrictions in [How to label data](/docs/discovery-data?topic=discovery-data-information-security#labeling)) to the optional `X-Watson-Metadata` header. {{site.data.keyword.discoveryshort}} can then delete it by `customer_id`.

On any REST call, an optional header `X-Watson-Metadata` can be sent with semicolon separated `field=value` pairs, where currently only `customer_id` is persisted. By adding that `customer_id` in `X-Watson-Metadata` header, the request indicates that it contains data that belongs to this `customer_id`.

`customer_id`s are unique within a single {{site.data.keyword.discoveryshort}} instance. They are not unique per environment or collection. Do not include personal data in these IDs.

Experimental and beta features are not intended for use with a production environment and, therefore, are not guaranteed to function, as expected, when labeling and deleting data. Do not use experimental and beta features when implementing a solution that requires the labeling and deletion of data.
{: note}

## Methods that support labeling data
{: #pi_methods}

The following stored information can be deleted using a `customer_id` if the `customer_id` was specified when the information was originally added using the associated method:

- queries (`/v2/environments/{environment_id}/collections/{collection_id}/query`) Only when used with the `passages` or `natural_language_query` parameters
- events (`/v2/events`)
- documents (`/v2/environments/{environment_id}/collections/{collection_id}/documents`)
- notices (`/v2/environments/{environment_id}/collections/{collection_id}/notices`) Only ingestion `notices` are labeled.
- training data (`/v2/environments/{environment_id}/collections/{collection_id}/training_data`)

The following stored information is not explicitly labeled and cannot be deleted by specifying the `customer_id`. Personal Data is not supported in these fields.

Any string fields (including but not limited to `name` and `description`) of the following stored items:
- configurations
- collections
- environments

## Labeling data
{: #labeling}

When ingesting documents, include the `X-Watson-Metadata` header using the `POST /v2/environments/{environment_id}/collections/{collection_id}/documents` or `POST /v2/environments/{environment_id}/collections/{collection_id}/documents/ID` operations. The `customer_id` field is added to the `extracted_metadata` of the documents. Your application must be configured to provide a `customer_id` in the `X-Watson-Metadata` header when performing any operation.

Optionally, you can include the `customer_id` field with the `metadata` multi-part form part instead of using the `X-Watson-Metadata` header.

If your documents are already ingested, you must reingest them to add the `X-Watson-Metadata` header and `customer_id`.
{: note}

If you specify a `customer_id` in the `metadata` multi-part form part and the `X-Watson-Metadata` header for the same document, then the `customer_id` in the `X-Watson-Metadata` header is used.
{: note}

Restrictions:

- The value of the `X-Watson-Metadata` header cannot exceed 4 kilobytes of text.
- The `X-Watson-Metadata` header must contain a semicolon separated list of `field=value` pairs. The `field` and `value` must not contain semicolons (`;`) or equals signs (`=`).
- `customer_id`s are unique within each {{site.data.keyword.discoveryshort}} instance. They are NOT unique per environment or collection.
- A `customer_id` cannot be more than 256 characters in length.
- If a `customer_id` contains only whitespace or is empty, it is treated as though the `customer_id` was not provided at all, and no error messages are returned.

### Labeling data with the Discovery tooling
{: #labelingtooling}

Data can be labeled with the `customer_id` field, when you use the {{site.data.keyword.discoveryshort}} tooling. Click the ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> and enter the `customer_id` in the **GDPR Data Label** field. After this field is set, all data uploaded using this browser session is labeled with the specified `customer_id`. If the associated customer ID changes, change this field.

Adding a `customer_id` with the **GDPR Data Label** field labels the documents, notices, and training data within that URL domain from that point forward, including each instance under that domain. Any actions, including document uploads, that occurred in the {{site.data.keyword.discoveryshort}} tooling before adding the **GDPR Data Label** field are not labeled.

If you switch domains or browsers, empty the browser cache, or start an incognito session after you specify your `customer_id` using the **GDPR Data Label** field of the {{site.data.keyword.discoveryshort}} tooling, the `customer_id` is not retained, and your data is not labeled. If you must switch domains or browsers, re-enter the `customer_id` in the **GDPR Data Label** field.
{: note}

## Deleting labeled data
{: #deletingdata}

To delete it later, data must be labeled with a `customer_id`.

1. Use the `DELETE /v2/user_data` operation and provide the `customer_id` of the data you wish to delete. `DELETE /v2/user_data` deletes all data associated with a particular `customer_id` within that service instance, as specified in [Methods that support labeling data](/docs/discovery-data?topic=discovery-data-information-security#pi_methods). Also see the [API reference](https://{DomainName}/apidocs/discovery-data#delete-labeled-data){: external}

Deletions are performed asynchronously. You cannot track the progress of deletions.

To ensure all labeled content is correctly removed, run `user_delete` after the `processing` and `pending` counts for all collections in your environment return `0`.

If a non-existent `customer_id` is provided, nothing is deleted, but a `200 - OK` response is returned.

Environments and Collections are not labeled with a `customer_id`, even if a `X-Watson-Metadata` header is included in the request to create the environment or collection. Only the individual documents within a collection within an environment are labeled. Therefore when data is deleted, individual environments and collections are NOT deleted.

You cannot delete labeled data using the {{site.data.keyword.discoveryshort}} tooling.