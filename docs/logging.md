# Logging and Troubleshooting

Each process in the application - the controller and each worker - generate their own log file. In addition, the workers create a log file for each export job containing a subset of the messages that are made available to users through the GO button for the Logfile attribute in the UI.

There are three main types of messages that end users see in the log files:
 - INFO: are informational messages. No action is required.
 - WARN: are warnings that indicate that situation that was faced was not ideal. For most instances, no action may be required, but some circumstances may be fixed.
 - ERROR: are severe errors that caused a component to fail or a process was prevented from doing its thing. Some errors are reported and the job continues. Other errors may cause the export to fail.

When a severe error or a code exception occurs, additional information along with a stack trace are dumped on the worker (or controller) log file. These messages are not sent to the user-facing log files.

In addition, there are two _debug_ flags in the application.properties files that can flipped, which will cause additional application debug messages and database queries to be logged.

So, dev-ops personnel or administators are advised to look in the worker logs to better understand and debug edge cases and errors.

## Error messages and suggested fixes, if any

Most error messages are self-explanatory. Dev-ops and/or administrators may use the stack trace along with the file in which the error appears to determine the best course of action to fix any issues that they're trying to solve. The following is a detailed listing of all error messages (as of 7/1/2021). Here, {0}, {1}, and so on represent placeholders for values that will be filled in at runtime.

### exports-core

#### Source file: **ApiService**
 - Unable to authenticate!
 - {0}: {1}\n{2}, e.getStatusCode, e.getStatusText, e.getResponseBodyAsString
 - Unable to update item {0}. {1}: {2}\n{3}
 - Unable to delete items {0}. {1}: {2}\n{3}
 - Unable to get data from API

#### Source file: **CodeSetRepositoryExtendedImpl**
 - Attribute {0} is not linked to a codeset
 - Code set {0} is not found.
 - Code set {0} does not have any values.

#### Source file: **ExportConfigurationRepositoryExtendedImpl**
 - Could not find member with ID {0}
 - Could not find hierarchy named {0}

#### Source file: **ExportScheduleRepositoryExtendedImpl**
 - Cannot calculate NextExecutionTimestamp. Frequency is blank.
 - Quarterly is not yet implemented, unfortunately!
 - Unknown Schedule Type: {0}

#### Source file: **MasterRepositoryItemRepositoryExtendedImpl**
 - Unable to parse XML for bMasterRepositoryItem {0}
 - Duplicate attribute {0} for language {1} in item {2}
 - Unknown attribute {0} for profile {1}
 - Unknown node {0} for item {1}
 - Unknown attribute ID {0} for item {1}

#### Source file: **Utilities**
 - All inputs to coalesce are null!
 - Retrying attempt {0} of 3

### exports-controller

#### Source file: **MessageSender**
 - There are {0} workers currently running. Please stop them first.
 - Cannot send a message with a null object.
 - Unable to serialize object {0} {1}

#### Source file: **ScheduleTask**
 - Found an illegal/improperly formed Export Schedule record. Potentially, ID is not populated.
 - Could not enqueue Schedule with ID: {0}

### exports-worker

#### Source file: **HierarchyDefinitionExportService**
 - Could not pivot Attribute Names.

#### Source file: **ItemDataAndDigitalAssetsExportService**
 - Zero records would be in the export. Nothing to do.
 - Could not read {0}. Not converting to Excel.
 - Could not delete {0}
 - Unable to find search configuration with name {0} in {1} repository
 - Could not download assets.
 - Could not rename Value and UOM columns.
 - Saved Set Name is empty when Filter is set to Saved Set. Please fix one of these two parameters. Not applying Saved Set filter.
 - Saved Search Name is empty when Filter is set to Saved Search. Please fix one of these two parameters. Not applying Saved Search filter.
 - At least 1 global attribute must be specified. Alternatively, turn off global attributes in Export Configuration.
 - Could not read data from {0} repository
 - Could not concatenate Value and UOM columns.
 - Could not pivot Values with Attribute headers.
 - Could not pivot Attribute, Value and UOM columns.
 - Could not join item data components.
 - Could not split item data.

#### Source file: **ItemExportForMemberData**
 - Unknown Data Source!
 - Could not join Member SKU and AD SKU global attributes.
 - Could not join Member and AD SKU Values.
 - Could not join Member SKU and Member SKU Values.
 - Could not join Member SKUs and AD SKU Values.
 - Could not Coalesce Member SKU and AD SKU global columns.
 - Could not Coalesce Member SKU and AD SKU category attribute columns.

#### Source file: **ManufacturerBrandExportService**
 - Could not lookup codesets for Manufacturer and Brand

#### Source file: **SpecialValueCalculatorForCompetitor**
 - Could not concatenate Value and UOM columns.

#### Source file: **SpecialValueCalculatorForProduct**
 - {0} is not yet supported.

#### Source file: **SpecialValueCalculatorForTaxonomy**
 - Cannot prefetch Hierarchy: Taxonomy name is set to blank.

#### Source file: **SpecialValueCalculatorForWholesaler**
 - Could not concatenate Value and UOM columns.

#### Source file: **TestExportService**
 - Unable to copy test file to target directory

#### Source file: **AdOrMemberBasedEntityRepository**
 - {0} query is not defined for {1}
 - No queries found for attribute source {0} for target table {1} with temp table {2}

#### Source file: **SkuAssets**
 - Unknown column {0}. Expecting 'image' or 'document' in name
 - Unknown column {0}. Expecting 'filename' or 'caption' in name
 - Unknown level in column {0}

#### Source file: **TaxonomyEntity**
 - Unknown level in {0}
 - {0} is not supported yet.

#### Source file: **MessageProcessor**
 - Unable to properly read message into Export Entity: {0}
 - Export configuration {0} has gone missing! Cannot run a non-existent task.
 - Export of type {0} is not yet supported.
 - Export errored out for {0}
 - Schedule {0} has gone missing!

#### Source file: **ExportService**
 - Aborted job {0} for export job {1}.
 - Unable to send email
 - Unable to export files to FTP.
 - Could not delete {0}
 - Unable to send files to S/FTP.
 - Could not process special characters.

#### Source file: **Processor**
 - Ignored {0} null records!

#### Source file: **CoalesceColumns**
 - The first attribute in all column sets are empty in line {0}. Defaulting to use primary columns.
 - At least two primary columns expected for Key, Value, etc.
 - Equal number of columns in primary and secondary columns is required.
 - Equal number of columns in primary and tertiary columns is required.
 - Equal number of columns in primary and output columns is required.

#### Source file: **ConcatenateAttributes**
 - At least one set of columns must be provided

#### Source file: **DownloadAssets**
 - Unknown DAM Variant {0}
 - Unable to zip files into {0}

#### Source file: **HandleSpecialCharacters**
 - Unknown Special Character Handling Option {0}. Fallback to using UTF8 characters.

#### Source file: **JoinRecordsets**
 - None of the sources were processed in this iteration.
 - None of the sources were processed in this iteration.
 - Exactly two inputs are required for one-to-many joins
 - At least one key must be defined
 - No of keys must be the same for all inputs

#### Source file: **LookupCodesets**
 - Unknown attribute {0} in profile {1}

#### Source file: **ReadItemsFromRepository**
 - {0} is not supported yet.
 - Invalid code {0} not found in codeset {1}

#### Source file: **SaveToFile**
 - Unable to create directory {0}
 - Only Csv, Tab and Excel files are supported right now. Falling back to CSV.
 - File {0} already exists. Append is not allowed. Skipping.
 - Header values do not match. Cannot (should not) append to existing file {0}
 - File {0} already exists.

#### Source file: **SendEmail**
 - Invalid email address {0} - {1}

#### Source file: **SplitDataset**
 - Unable to parse integer from {0}. Falling back to 0.
 - Missing required attribute to split on: {0}. Please include it in export mapping.
