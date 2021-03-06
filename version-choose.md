---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-15"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:preview: .preview}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:table: .aria-labeledby="caption"}

# Getting the most from Discovery
{: #version-choose}

Use the latest version of {{site.data.keyword.discoveryshort}} to take advantage of new features and a simpler way to build solutions.
{: shortdesc}

When you create a Premium or Plus (including a Plus Trial) plan instance on {{site.data.keyword.cloud_notm}}, you get the latest version of the {{site.data.keyword.discoveryshort}} user interface. The latest version uses version 2 of the {{site.data.keyword.discoveryshort}} API. The same is true when you install and provision an instance on {{site.data.keyword.icp4dfull_notm}}; you get the latest version.

The earlier version was provisioned for you previously when you created a Lite or Advanced plan instance on {{site.data.keyword.cloud_notm}}. The earlier version of the {{site.data.keyword.discoveryshort}} user interface uses version 1 of the {{site.data.keyword.discoveryshort}} API.

## Advantages of using the latest version
{: #version-choose-v2-highlights}

The latest version offers the following features and enhancements:

- A project-based experience that supports many different use cases within a single environment.
- Built-in customization tools for adding dictionaries, patterns, and classifiers to help business users build projects that understand the language of their domain.
- Connectors to popular data sources that can quickly access valuable data where it resides.
- Smart Document Understanding that learns from the structure of human-readable documents, such as PDFs.
- Natural language query support across all document types, optimized with machine learning to find targeted answers.
-	Advanced search capabilities, such as answer finding, curations, and table retrieval.
- An out-of-the-box contract understanding function that helps you search and interpret legal contracts.
- A full-featured Content Mining application that you can use to conduct in-depth analysis of unstructured text.
- Customizable user interface components that help you to deploy custom applications.

## Comparing v1 and v2 features
{: #version-choose-comparison}

If you are already familiar with the earlier version of the product, learn more about how the latest version compares.

The latest version has new features that were previously unavailable. The following table describes feature support in both versions right now.

| Feature | Latest version (v2) | Earlier version (v1) |
|---------|---------------------|----------------------|
| Use projects to organize your work | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Create a content mining project type and then use the built-in Content Mining application to do in-depth data analysis (*{{site.data.keyword.icp4dfull_notm}} and Premium plans only*) | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Apply the Parts of Speech enrichment to your data | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Leverage intuitive user interface tools to add domain-specific artifacts, such as dictionaries and custom machine learning models | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Perform real-time NLP with the Analyze API (*{{site.data.keyword.icp4dfull_notm}} only*) | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Apply a pre-trained Smart Document Understanding model to your collection for similar benefits with less effort | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Extract meaning from tables | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Retrieve tables | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Advanced question-answering capabilities, such as extracting FAQs and highlighting the exact answer (beta features) | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| You can enable optical character recognition (OCR) to process text from scanned documents or other images | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Support for more connectors from a {{site.data.keyword.icp4dfull_notm}} deployment, including databases, file systems, FileNet P8, and HCL Notes | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Some connectors support document-level security from a {{site.data.keyword.icp4dfull_notm}} deployment | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Get insights from contracts (*{{site.data.keyword.icp4dfull_notm}} and Premium plans only*) | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Use the Entity Extraction, Sentiment Analysis, and Keyword Extraction enrichments | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Discovery Query Language (DQL) API support | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Use the Smart Document Understanding (SDU) to annotate your documents | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Retrieve passages from documents | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Apply Watson Knowledge Studio NLP models to your data | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Perform relevancy training to improve query results | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Configure continuous relevancy training | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Use the Watson Discovery News and COVID-19 collections to leverage pre-enriched data | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Identify document similarity | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Configure the normalization process of ingestion | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Use the Category classification, Concept tagging, Relation Extraction, Emotion Analysis, and Semantic Role Extraction enrichments | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Review query logging and metrics | | ![checkmark icon](../../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Feature support details" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify features. The column headers identify the different versions of the product. To understand which features are supported by a product version, go to the row that describes the feature, and find the column for the product version that you are interested in."}

## Limit details
{: #plan-limit-links}

For more information about artifact limits per plan, see the feature documentation:

- [Advanced rules model limits](/docs/discovery-data?topic=discovery-data-domain#advanced-rules-limits)
- [Classifier limits](/docs/discovery-data?topic=discovery-data-domain#classifier-limits)
- [Collection limits](/docs/discovery-data?topic=discovery-data-collections#collections-limits)
- [Dictionary limits](/docs/discovery-data?topic=discovery-data-domain#dictionary-limits)
- [Document limits](/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits)
- [Machine Learning model limits](/docs/discovery-data?topic=discovery-data-domain#machinelearning-limits)
- [Pattern limits](/docs/discovery-data?topic=discovery-data-domain#patterns-limits)
- [Project limits](/docs/discovery-data?topic=discovery-data-projects#projects-limits)
- [Query limits](/docs/discovery-data?topic=discovery-data-query-concepts#query-limits)
- [Regular expression limits](/docs/discovery-data?topic=discovery-data-domain#regex-limits)
- [SDU limits](/docs/discovery-data?topic=discovery-data-configuring-fields#sdu-limits)

The following limits apply only to Content Mining project types:

- [Document classifier limits](/docs/discovery-data?topic=discovery-data-contentminerapp#doc-classifier-limits)
- [Regular expression pattern limits](/docs/discovery-data?topic=discovery-data-contentminerapp#regex-limits)
