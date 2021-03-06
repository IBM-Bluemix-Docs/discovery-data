---

copyright:
  years: 2019, 2021
lastupdated: "2021-06-24"

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
{:external: target="_blank" .external}


# Windows File System
{: #connector-wfs-cp4d}

Crawl documents that are stored in a Microsoft Windows file system.
{:shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

## What documents are crawled
{: #connector-wfs-cp4d-docs}

- Only documents that are supported by {{site.data.keyword.discoveryshort}} in your file path are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- Document level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they access the file system directly.
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-wfs-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your Windows File System data source must meet the following requirements:

- The connector supports Microsoft Windows Server 2012 R2, 2016, and 2019.
- The remote agent server and the file servers to be crawled must belong to the same Windows domain. The crawler can gather access control list (ACL) data from a single Windows domain only.

## Prerequisite steps
{: #connector-wfs-cp4d-prereq}

- If you want to enable document level security, you must take some steps to set it up. For more information, see [Supporting document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
  
  To configure document level security, you need to collect the following information:
  
  - **LDAP server URL**: The LDAP server URL to connect to. For example, `ldap://<ldap_server>:<port>`.
  - **LDAP binding username**: The username to use to bind to the directory service. 
  
    In most cases, this username is a distinguished name (DN). An Active Directory username might work, but, unlike the general Windows logon, it is case sensitive.
    - **LDAP binding user password**: The password that is associated with the binding username.
    - **LDAP base DN**: The starting point for searching user entries in LDAP. For example, `CN=Users,DC=example,DC=com`. 
    - **LDAP user filter**: The user filter to search user entries in LDAP. If empty, the default value is `(userPrincipalName={0})`.

- Before you configure a Windows File System collection, you must install the agent server on a remote Windows file server or on a remote Windows server. The agent server is a Windows service that retrieves data from data source servers and sends it to {{site.data.keyword.discoveryshort}}. The Windows agent can crawl remote Windows file systems, drives that are local to the agent, and shared network folders.

  If you install the agent server on a remote Windows server, the remote Windows server must be able to mount one or more file servers so that the agent can crawl remote Windows file systems. 

  To install and configure the agent server, complete the following tasks:

  - [Install the agent server](#connector-wfs-cp4d-prereq1).
  - [Configure shared directories on the agent server](#connector-wfs-cp4d-prereq2).
  - [Start and monitor the status of the agent server](#connector-wfs-cp4d-prereq3).

### Install the agent server
{: #connector-wfs-cp4d-prereq1}

To install the agent server, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Windows File System**, and then click **Next**.
1.  Scroll to the *Download & install Windows Agent* section, and then click **Download Windows Agent Installer**.

    A ZIP file is downloaded.
1.  Extract the files from the `WindowsAgentServer.zip`.
1.  You can choose one of the following methods to run the installation program:

   - Double-click the `install.exe` file to launch the installation wizard.

   - To run the installation program in text mode from a console, complete the following steps:

     1. Change to the agent directory.
     1. Enter the following command:

         ```bash
         install.exe -i console
         ```
         {: pre}

        The screens are rendered in text and prompt you for the same information as the graphical installation.

        After you enter the command, a process runs in the background for several seconds before the console installation program is displayed.
        {: note}

   - To install the agent server silently, complete the following steps:

     1.  Change to the `Agent/responseFiles` directory.
     1.  Edit the `DistributedFileSystemCrawler.properties` template response file to provide information about your environment. To run the installation program, change to the agent directory, and then specify the name of the file that you edited. 
     
          See the following example:
         
          ```bash
          install.exe -i silent -f responseFiles/DistributedFileSystemCrawler.properties
          ```
          {: pre}

      If you copy a template file to another location to edit, specify the fully qualified path for the file when you run the installation program. If the response file path includes a space, enclose the path in double quotation marks (`"`). See the following example:
      ```bash
      install.exe -i silent -f "c:\My Documents\DistributedFileSystemCrawler.properties"
      ```
      {: pre}

1.  You must provide the following information during the installation process:

    - `hostname`: Enter or verify the fully-qualified hostname of the computer you are installing the agent server on.

      You cannot specify an IPv6 address as the hostname of the server.
      {: important}
    - `username`: Enter the username of an account that can be used to authorize access to the agent server. 
    
      If the username does not exist, select the checkbox to create the account.

      To crawl a domain in a secure collection, the username must be an existing domain user with administration privileges for the Windows system to be crawled. To specify a domain user, use the format `<username>@<domain name>`. 
      {: important}
    - `password`: Provide the password that is associated with the username.

1.  **Optional**: If you want to change the default path and port settings, click **Advanced Options**.

    - You can change the paths for the installation directory and data directory.
    - The agent server uses three TCP/IP ports for authenticating connections to the server, transferring data between the file systems and {{site.data.keyword.discoveryshort}}, and monitoring the agent server. The default port numbers are `8397` and `8398`. If those values conflict with other port assignments in your system, change the port numbers.
1.  On the summary page, review the options that you selected, and click **Install** to start installing the software.
1.  Restart your computer.

### Configuring shared directories on the agent server
{: #connector-wfs-cp4d-prereq2}

After the software is installed, you must set up shared network directories that the Windows File System agent can access. To define a new file system share, export a local or remote network directory. You can also reuse a share that was defined previously.

1. Export a local directory from the server where the agent is installed:

   ```bash
   esagent --addshare <d:><\example>
   ```
   {: pre}

   Where `d:` represents the drive letter you want to use and where `\example` represents the path to the local directory.
1. Export a remote network directory that is accessible from the server where the agent is installed:

   ```bash
   esagent --addshare <\\files.example.com\data>
   ```
   {: pre}

   Where `\\files.example.com\data` represents the hostname or IP address of the remote server or the path to the remote directory. 
1. List shares that are defined on the server where the agent is installed:

   ```bash
   esagent --lsshare
   ```
   {: pre}

1. If you want to delete a share that is defined on the server where the agent is installed, you can use the following command:

   ```bash
   esagent --rmshare \\files.example.com\data
   ```
   {: pre}

### Server status commands
{: #connector-wfs-cp4d-prereq3}

After you install the agent server, you can enter commands to start, stop, and check the status of the server. 

Stopping the agent server also stops the crawler. For example, if the crawler stops unexpectedly, you can close connections and release resources for that crawler.

- To start the server, enter the following command:

  ```bash
  esagent start
  ```
  {: pre}

- To stop the server, enter the following command:

  ```bash
  esagent stop
  ```
  {: pre}

- To get the status of the agent server, enter the following command:

  ```bash
  esagent getStatus
  ```
  {: pre}

The output of the `getStatus` command is an XML file with the following output:

```bash
<AgentStatus>
  <SpaceStatus>
    <SpaceId>012</SpaceId>
    <RootFolder>E:\\Projects\Analytics\\data\test1</RootFolder>
    <ConnectionNumber>9</ConnectionNumber>
    <StartTime>1244709336093</StartTime>
    <LastTime>1244709385843</LastTime>
    <IdlePeriod>219</IdlePeriod>
  </SpaceStatus>
  <SpaceStatus>
    <SpaceId>013</SpaceId>
    <RootFolder>E:\\Projects\Analytics\\data\test2</RootFolder>
    <ConnectionNumber>10</ConnectionNumber>
    <StartTime>1244709336093</StartTime>
    <LastTime>1244709385843</LastTime>
    <IdlePeriod>219</IdlePeriod>
  </SpaceStatus>
  ```
  {: screen}

## Connecting to a Windows File System data source
{: #connector-wfs-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps. 

If you completed the prerequisite steps, return to the Windows File System data source collection that you started to create, and then skip to Step 4.
{: note}

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Windows File System**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents that you want to crawl is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule. 

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Enter your credentials* section, add values to the following fields. You provided these fields during the installation of the agent server, which was described in the [Prerequisite steps](#connector-wfs-cp4d-prereq) section.

    - **Host**: The hostname of the remote Microsoft Windows server, for example `<hostname>.mydomain.com`.
    - **Username**: The username to connect the agent server. You use the username to connect {{site.data.keyword.discoveryshort}} to the shared network folders and crawl content.
    - **Password**: The password that is associated with the username.
    - **Agent Authentication Port**: The port to use for authentication. The default port value is `8397`.
    - **Port**:  The port to use for transferring data. The default port value is `8398`.
1.  In the *Specify what you want to crawl* section, enter the file path that you want to crawl in the **Path** field, and then click **Add**. 

    The file path is case sensitive.
1.  Optionally, add more file paths.
1.  **Optional**: If you want to enable document level security, in the *Security* section, set the **Enable Document Level Security** switch to `On`.

    When you enable this option, your users can crawl and query content that they have access to. You must provide the details about the LDAP directory you want to use.

    - **LDAP server URL**: The LDAP server URL to connect to. For example, `ldap://<ldap_server>:<port>`.
    - **LDAP binding username**: The username to use to bind to the directory service.
    - **LDAP binding user password**: The password that is associated with the binding username.
    - **LDAP base DN**: The starting point for searching user entries in LDAP. For example, `CN=Users,DC=example,DC=com`. 
    - **LDAP user filter**: The user filter to search user entries in LDAP. If empty, the default value is `(userPrincipalName={0})`.
1.  If you want the crawler to extract text from images in documents, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}
1. Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection. 

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
