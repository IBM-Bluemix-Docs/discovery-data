---

copyright:
  years: 2019, 2021
lastupdated: "2021-07-14"

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
{:video: .video}

# Adding custom fields with Smart Document Understanding
{: #configuring-fields}

Use Smart Document Understanding (SDU) to teach {{site.data.keyword.discoveryfull}} about other fields in your documents that contain meaningful information. When you help {{site.data.keyword.discoveryshort}} index the correct set of information in your documents, you improve the answers that your application can find and return.
{: shortdesc}

This video provides a quick overview of Smart Document Understanding:

![Watson Discovery Demo: Extract Answers From Large Documents in 5 Minutes](https://www.youtube.com/embed/Jpr3wVH3FVA){: video output="iframe" data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

To view the transcript, open the video on YouTube.

Documents come in all shapes and sizes. Your collection might have a mix of different document structures. Pick a subset of documents from your collection that are representative of the different document structures in use. You will use this representative set of documents to train Watson to recognize custom fields that contain meaningful information.

As you annotate the representative documents, Watson learns and starts to predict annotations.

## When to use Smart Document Understanding
{: #sdu-when}

The Smart Document Understanding (SDU) tool works better with some project types.

- The tool is most beneficial when used with *Document Retrieval* projects. Use it to add custom fields to [the set of fields that are indexed by default](#sdu-default-fields).
- *Document Retrieval for Contracts* projects apply a custom SDU model to the documents in your collection automatically. It basically does the work for you. Instead of making you annotate contract-related content in your documents, it uses a pretrained SDU model that already knows how to recognize terms and concepts that are significant to contracts. As a result, you cannot apply a user-trained SDU model to this project type, but you also don't need to.
- The best way to prepare a collection for use in *Conversational Search* projects is to identify discrete question-and-answer pairs. You can use the SDU tool to find and annotate them. 
  
  ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Try out the FAQ extraction feature, which basically does the work of identifying question-and-answer pairs for you, but is available as a beta and therefore is not appropriate for production use.
- The SDU tool is not often used with *Content Mining* projects.

The SDU tool can annotate the following file types only:

- Image files (PNG, TIFF, JPG)
- Microsoft PowerPoint
- Microsoft Word
- PDF

For a complete list of file types that {{site.data.keyword.discoveryshort}} supports, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).

The tool cannot read documents with the following characteristics; remove them from your collection before you begin:

- Documents that appear to have text that overlays other text are considered “double overlaid” and cannot be annotated.
- Documents that contain multiple columns of text on a single page cannot be annotated.

To access the Smart Document Understanding editor:

- Open your project and select the **Improve and customize** icon on the navigation panel. On the **Improvement tools** panel, select **Define structure** and choose **New fields**. If your project contains more than 1 collection, you can then choose the collection.
or
- Select the **Manage collections** icon on the navigation panel and open a collection. For more information on collections, see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections).

When you build a custom Smart Document Understanding model, the conversion time for your collection may increase due to the resources required to apply the AI model to your documents. The resource requirements will result in a significant decrease in throughput speed.
{: note}

To navigate the Smart Document Understanding editor, view the following information:

1. On the **Manage collection** page, there are three tabs that are needed to use Smart Document Understanding: **Identify fields**, **Manage fields**, and **Enrichments**.

   - **Identify fields** - the SDU tool
   - **Manage fields** - see [Managing fields](#field-settings)
   - **Enrichments** - see [Managing enrichments](/docs/discovery-data?topic=discovery-data-managing-enrichments)

1. Open the **Identify fields** tab. A subset of documents will be available for annotation purposes. Between 20 - 50 documents will appear in the dropdown list. The number will depend on several factors, including the number of documents in your collection in the supported file formats. 

Use the SDU toolbar to perform the following tasks:

- Choose a document to annotate
- Navigate the document displayed
- Adjust the page view (`single page view`, `zoom in`, `zoom out`), `clear changes`, and `export/import models`. Click on `single page view` to toggle the display. You can view your annotations and document separately or together.

Also see [Getting started with {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-getting-started).

## Identifying fields
{: #identify-fields}

<!-- c/s help for the **Identify fields** tab. Do not delete.  -->

1.  Open the **Improve and customize** page from the navigation panel. On the *Improvement tools* panel, expand *Define structure*, and then choose **New fields**.
1.  If your project has more than one collection, select the collection with documents that you want to annotate.
1.  Choose the type of model you want to use:

    - **Text extraction only**: Any text that is recognized in the source document is indexed in the `text` field. This option is selected by default because it is applied to all collections unless you choose to use a model.
    - **User-trained models**: Opens the Smart Document Understanding tool that you can use pick certain types of text to store in fields other than the `text` field.
    - **Pre-trained-models**: Applies a non-customizable model that extracts text and identifies tables, lists, and sections. This model converts table information to HTML format, so you can apply the [Understanding tables](/docs/discovery-data?topic=discovery-data-understanding_tables) enrichment to the `html` field.
1.  Click **Submit**, and then click 
1.  Click **Apply changes and reprocess**.

If you selected **User-trained models**, a subset of documents is available for you to annotate. A set of 20 - 50 documents is displayed in a list. The number of documents that are available differs based on several factors, including the overall number of documents in your collection and how many of them are supported file types. Continue to the [Annotating documents](#sdu-task) procedure.

See [Best practices for annotating documents](/docs/discovery-data?topic=discovery-data-configuring-fields#bestpractices) before you begin annotating.

### Annotating documents
{: #sdu-task}

1.  Review the field labels that you can use to annotate the document. They are displayed in the *Field labels* panel.

    See the *Default field labels* table for a list of the fields and their descriptions.
1.  To create a custom field label, click **Create new**. 

    - Specify a field label with lowercase letters and no spaces. For example, `my_field` is a valid field label.
    - If you want to change the color that will be used to represent the field, repeatedly click the color block ![Square block of color with two arrows that point in a circle](images/sdu-label-color.png) until it is displayed in the color that you want to use.
    
      You cannot change the field label color later.
      {: important}
    - Click **Create**.
1. To begin annotating the document, click a field label to activate it.
1. Click the content representing that field in the SDU tool. Alternately, you can select a field label and drag it to the content in the SDU tool.

   The content is highlighted. To undo an annotation, click the **Clear changes** button on the toolbar.
1. Click the **Submit page** button.
   
   As you annotate, Watson is learning and starts to predict annotations. Continue annotating until Watson correctly and consistently identifies fields.
   {: note}
   
1. When you have completed annotating, click the **Apply changes and reprocess** button.

### Fields indexed by default
{: #sdu-default-fields}

The following fields make up the base set of fields that {{site.data.keyword.discoveryshort}} is designed to recognize and index by default.

| Field | Definition |
|-------|------------|
| answer | In a Q/A pair (often in an FAQ), the answer to the question. |
| author | Name of author (or authors). |
| footer | Use this tag to denote meta-information about the document (such as the page number or references), that appear at the end of the |page. |
| header | Use this tag to denote meta-information about the document that appears at the start of the page. |
| question | In a Q/A pair (often in an FAQ), the question. |
| subtitle | The secondary title of the document being annotated. |
| table_of_contents | Use this tag on listings in the document table of contents. |
| text | Use this tag for standard copy text, including paragraphs, definitions, or any set of words that is not a title, part of a table, answer, author, subtitle, header, or a footer. |
| title | The main title of the document being annotated. |
| table |	Use this tag to annotate tables in your document. |
| image |	Use this tag to annotate images and diagrams in your document. |
{: caption="Default field labels" caption-side="top"}

When you annotate one or more tables using the `table` field, you will automatically enable the **Table Understanding** enrichment for the entire collection. The **Table Understanding** enrichment is applied to the `html` field of your collection. For more information, see [Understanding tables](/docs/discovery-data?topic=discovery-data-understanding_tables).
{: #important}

### Best practices for annotating documents
{: #bestpractices}

If you want to save time reprocessing all the files in a large collection, start with a small collection of documents and build your model, then [export](/docs/discovery-data?topic=discovery-data-configuring-fields#import) it. Create a new collection that contains only 1 document, import the model, then upload the remainder of your documents.
{: tip}

- Follow all guidelines and use consistent labeling on all documents
- Do not label whitespace
- Do not treat **bold**, _italic_, or underlined text differently. Label based on the context, not the style.
- When labeling a document, work from the first page to the last.
- If you incorrectly label an item, choose another label for the item to overwrite the first.
- Pages can be submitted at any time. Ensure that all appropriate labeling is complete before submitting.
- When annotating a table, make sure to select the entire table before applying the `table` label.

If `Run OCR` is enabled when you create your collection, text is extracted from images using Optical Character Recognition (OCR). If you do not want to apply this option for specific images or diagrams, apply the `image` label to those images.
{: important}

### Importing and exporting SDU models
{: #import}

After you define a model with the SDU tool, you can save it and reuse it on other collections.

You can import or export your completed SDU model using the toolbar in the header of the editor. Click the last icon and choose `Import model` or `Export model`.

Exported models have the file extension of `.sdumodel`.

An imported model is intended to be used without any further annotations. The model will be completely overwritten if you continue annotating after importing it.

If you plan to develop a model and import it into a new collection, it is a sound best practice to create a new collection that contains only 1 document, import the model, then upload the remainder of your documents.
{: tip}

## Managing fields
{: #field-settings}

<!-- c/s help for **Manage fields** page. Do not delete. -->

The **Manage fields** tab contains several options:

-  **Identify fields to index**: For more information, see [Preventing content from being returned in results](/docs/discovery-data?topic=discovery-data-hide-data).
-  **Improve query results by splitting your documents**: For more information, see [Split documents to make query results more succinct](/docs/discovery-data?topic=discovery-data-split-documents)
-  **Date format settings**

To access the **Manage fields** page, click the **Manage collections** icon on the navigation pane and open a collection. Click the **Manage fields** tab. For more information on collections, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections).

**Date format settings**: The following options are useful if you want to use time series visualization in the **Content Mining** project type or if you want to correctly parse dates from text in different languages. You can add or delete date formats that are used to convert date strings to date-type data set fields. Only strings that are compatible with the Java `SimpleDateFormat` class are supported. You cannot add any documents that include alternative date formats to the index.

  - **Date formats**: Use this option to parse a string representation into the `Date` data type. For example, `Sun, 06 Nov 1994 08:49:37 GMT`, or `1994-11-06`, is parsed as the same date. This field supports the Java `SimpleDateFormat` class, so the date formats string can be in any format that the `SimpleDateFormat` class supports. If you know that your data does not match any of the predefined date formats, you can add a format that the Java `SimpleDateFormat` class supports, or you can delete any of the predefined formats. {{site.data.keyword.discoveryshort}} checks the date formats in order for each date-type data set field and uses the first format that successfully parses the field. Therefore, be sure to place the date format that you want to use at the beginning of the list. You must run a full crawl or a full import to apply any changes to documents that are currently in the data set.
  - **Select a time zone**: You can use this option to designate a time zone for a document that has a generated time but no time-zone information. You can use this option to store a document creation time into a date-type data set field. For example, if a document is generated on `1 January 2020 1:00 AM Eastern Standard Time (EST)`, the document metadata only stores `2020-01-01 01:00 a.m.`. In this case, {{site.data.keyword.discoveryshort}} cannot parse `2020-01-01 01:00 a.m.` because, without time-zone information that is associated with the document, `2020-01-01 01:00 a.m.` is not specific. Because `1 January 2020 1:00 AM Eastern Standard Time (EST)` and `1 January 2020 1:00 AM Pacific Standard Time (PST)` are different times, you must select **(GMT-05:00) Eastern Standard Time** as the time zone ID so that {{site.data.keyword.discoveryshort}} parses `1 January 2020 1:00 AM` with the EST time zone, as intended.
  - **Select a language**: Use this option to choose a language to parse a string value that represents the date for the date-type data set fields. You can also use this option to manage any cultural or language-specific patterns of the dates in your documents. For example, using the `EEE, MM dd, yyyy` format, the **English (United States)** locale can parse the string value of `"Wednesday, 07 01, 2020"`, and the **Japanese (Japan)** locale can parse the same string value of `"水曜日, 07 01, 2020"`.

## Smart Document Understanding limits
{: #sdu-limits}

The number of custom fields that you can create per Smart Document Understanding model depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Custom fields per SDU model |
|--------------|--------------------------------:|
| Cloud Pak for Data |                 Unlimited |
| Premium      |                             100 |
| Plus (includes Trial)  |                    40 |
{: caption="Custom field limits" caption-side="top"}

The maximum number of documents that you can annotate to train an SDU model per collection depends on your {{site.data.keyword.discoveryshort}} plan type. <!--KEEPING SINCE WE WILL BE ADDING A DIF NUMBER FOR LITE EVENTUALLY-->

| Plan | Documents per collection |
|--------------|--------------------------------:|
| Cloud Pak for Data |                        40 |
| Premium      |                              40 |
| Plus (includes Trial)  |                    40 |
{: caption="Training set limits" caption-side="top"}
