# Introduction

The Optimized Exports application was created To be able to extract large datasets of data for users by selecting attributes and values from multiple repositories. These are designed to be executed in a separate set of parallel processes independent of the core EnterWorks application. This enables users to export data concurrently while reducing the load on the core application. Most of the data is extracted by parsing the database records directly in the micro services and placing the values for attributes requested by users in one of multiple formats. Exports can be executed ad-hoc or run in a schedule as full or delta extracts. Files may be manually downloaded or sent to an S/FTP site. Users are notified when an export completes or if they are aborted for whatever reason.

This implementation of Optimized Exports, customized for Affiliated Distributors (AD), allows members to configure and schedule several data exports using a self-service and intuitive user interface. This is an enhancement to replace the existing process of using Scheduled Exports that are setup by AD Administrators, which is cumbersome to maintain and restrictive to configure. The result is that each member can setup multiple custom exports of their data from EnterWorks.

## Need for enhancement

As AD expands the number of members using EnterWorks, a full review and optimization of exports has been envisioned. The primary areas of consideration are as follows:

 - All member exports were previously predefined. There was no flexibility to select fields to include/exclude from the set of available global attributes.

 - All exports were previously only set up for ISD hierarchy. This has to be expanded to include members who are inducted into other divisions.

 - Members did not have the ability to map attribute names in exports, similar to how the import mapping tool works. We cannot use the Export Template functionality because there is no way to segregate them by user or member using security context.

 - The asset extraction tool that were developed was external to the EnterWorks application and cumbersome for members to use. There was no ability to send digital assets directly to SFTP.

Some of the advantages of this process are as follows:

 - Members will manage and schedule their own exports. This eliminates the need for AD administrators to create the Scheduled Exports and maintain them. This also reduces the clutter in the Scheduled Exports repository and limits it to system and other AD-scheduled exports.

 - Members can choose the source of the data they will extract – Member data only, AD data only, or Member data overrides AD data.

 - Category specific attributes may be exported in one of multiple formats – as Attribute-Value-UOM triplets, with Attribute Names as column headers, or in a separate file like the Category Attribute Values repository view.

 - Assets may be exported as links (faster) or as a downloadable zip file (slower).

 - As before, users may choose options for:
    - HTML Character Handling – UTF-8, HTML Entity Codes or Remove
    - Records that will be exported – Full, Delta, Saved Set, or Saved Search
    - Language – en or fr-CA
    - File Format – XLSX, TSV, CSV

 - Data may be sent directly to an S/FTP location or downloaded from the UI using the Download link/Go button from the Exports repository.

 - Exports may be scheduled using a few different options, including Weekly, Monthly or On Demand.

 - Previously, scheduled exports were executed serially (one at a time). The new process allows us to use multiple micro-services, which enables us to run several exports concurrently.

## Business process and user interface

The new process has been implemented as a set of micro-services that is custom developed for AD. Multiple instances of the micro-service have been deployed. The number of instances may be determined based on the expected demand and usage statistics after deployment. As of this writing, there is one controller and eight worker processes in the production environment. If more jobs are waiting to be executed, they are picked up in the order they were received. Deploying independent micro-services for these exports reduces the load on EPX/Services Framework to focus on non-member scheduled activities.

Two new self-service repositories have been created:

1. Export Configuration – contains definitions of exports that members can define and schedule. It houses options that members can select to fully customize their export. This repository is secured using user security context; so only users who belong to the same member/company are able to see each other’s export definition.

2.	Export Mapping – contains attribute mappings and aliases for global attributes that members can choose and map in their exports. Members may choose which global attributes they want in the repository, the order/sequence and what they want to call it in the export.

 - For category attributes, members can choose to export them, or not. We will not have the ability to choose, map or order category attributes. It are an all or nothing option, in the order defined in the Category Attribute Metadata repository.

 - Any user from the member organization are able to download the export from the Export Log repository.

 - For digital asset exports, the need for forcing members to use the utility will go away. However, having the option to extract links may be an attractive option for some members.

## Export log and download links

A log of all the exports that were executed are maintained in the Export Log repository along with links to download the exports. These are stored until an AD Administrator deletes them, i.e., there will not be a scheduled cleanup of the Export Log repository.

The records in Export Log are visible to the AD Administrators as well as Members. Members can only see exports based on their security context. A log of the exports will not be found or reported in the Job Monitor. The Status column provide the user information on their export (Queued, Processing, Completed, Error, or Cancelled).

The Download URL in the Export Log repository will provide links to download the export files and any assets zip files that may be requested. The exported data itself are available for download for up to 30 days after the export is executed. After this period, the download links will no longer function.

Members as well as AD Administrators are able to abort running jobs by setting the ‘Abort’ attribute to Yes.

## Notification

Upon the completion of an export job, a notification email will be sent to the email addresses listed in the export definition. This email will contain the overall job status along with key metrics including (but not limited to) the number of records included in each component of the export packet. If there was an error, additional detail will be included that provides more detail.
