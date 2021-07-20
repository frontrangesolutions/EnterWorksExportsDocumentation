# Export types and classes

The java project for *export-worker* is designed to be a set of classes called *processors* that perform specific tasks (like CompressFiles, ReadItemsFromRepository, etc), and a set of classes called *export services* that use the processors with specific parameters in a specific order depending on the configuration designed by the users in the UI.

## Export types built for AD

The following export types are built specifically for Affiliated Distributors. These classes use the Core components to extract data from specific repositories, transform them based on the configuration options and create datasets in the requested formats.

 - **CategoryAttributeMetadataExportService:** Provides an extract of the category attribute metadata for the hierarchy based on Member ID or specifically requested using Export Configuration. Each line in the export represents one attribute of a taxonomy node. The following columns are included in the export:
   - TaxonomyName
   - NumericCode
   - NodeName
   - AttributeName
   - DataType
   - AttributeType
   - ValueDelimiter
   - IsDifferentiator
   - DisplaySequence
   - EntityType
   - IsFilterable
   - FilterSequence
   - Print
   - Status

 - **CompetitorInformationExportService:** Extracts competitor data for a request Member. The following columns are included in the export:
   - MemberSkuId
   - ADSkuId
   - MemberPartNumber
   - CompetitorName
   - PartNumber

 - **HierarchyDefinitionExportService:** Extracts category attribute metadata with all attributes for a taxonomy node represented in a single line. The following columns are included in the export:
   - TaxonomyName
   - NumericCode
   - NodeName
   - Level1Code
   - Level1Description
   - ...
   - Level8Code
   - Level8Description
   - ... and up to 100 AttributeName label columns

 - **ManufacturerBrandExportService:** Extracts the manufacturers and their associated brands. The following columns are included in the export:
   - Manufacturer_Code
   - Manufacturer_Name
   - Brand_Code
   - Brand_Name
   - AD_Supplier_Partner
   - AD_eContent_Participant
   - Restricted_Brand

 - **MemberHierarchyExportService:** Extracts data that represents the classification of member SKUs to member-hierarchies. The following columns are included in the export:
   - Classification_Source - This can be one of the following values:
     - Member Hierarchy Node Link - SKUs and Products with their explicitly defined Member Hierarchy Nodes
     - Derived from Member Hierarchy Node Mapping - SKUs and Products with Member Hierarchy Nodes derived from the Member hierarchy Node Mapping
     - Derived from Member SKU - Products with Member Hierarchy Nodes derived from their SKUs
     - Derived from Member Product or Sibling Sku - SKUs with Member Hierarchy Nodes derived from their Product or sibling SKU
   - Member_Hierarchy_Node_ID
   - Member_Product_ID
   - Member_Product_Number
   - Member_Product_Description
   - Member_SKU_ID
   - Member_Part_Number
   - Member_Alternative_Part_Number
   - AD_SKU_ID
   - AD_Product_ID
   - Member_Hierarchy_Code
   - Member_Hierarchy_Name
   - Node_Code
   - Node_Description
   - Level_1
   - Level_1_Code
   - ...
   - Level_8
   - Level_8_Code

 - **ProductInformationExportService:** Extracts Product information for Member SKUs. The following columns are included in the export:
   - memberSkuId
   - adSkuId
   - memberProductNumber
   - memberProductDescription
   - adProductNumber
   - adProductDescription

 - **TaxonomyExportService:** Extracts the taxonomy for the divisional hierarchy of the requested Member. The following columns are included in the export:
   - TaxonomyName
   - NumericCode
   - NodeName
   - Level1Code
   - Level1Description
   - ...
   - Level8Code
   - Level8Description
   - LevelNumber
   - Sequence
   - CategoryImageName
   - Status
   - Description
   - HierarchyPath

 - **TestExportService:** is used primarily to test the S/FTP credentials. It places a sample test file in the configured target location.

 - **WholesalerInformationExportService:** Extracts competitor data for a request Member. The following columns are included in the export:
   - MemberSkuId
   - ADSkuId
   - MemberPartNumber
   - WholesalerName
   - PartNumber


### Item Data and Digital Assets Export Service
This export service extracts some or all of the following components of Member SKUs and/or their corresponding AD SKUs: SKU global attributes, category attributes, product information, competitor data, wholesaler data, hierarchy information, and digital assets (URLs, SKU-to-Asset Mapping and asset files). This is done using a set of configuration attributes specified in the Export Configuration repository. Members can control the order in which the global attributes are exported using the Global Attribute Mapping table.

There are three exports that export item data and assets, and are coded as a set of abstract and derived classes:
 - ItemDataAndDigitalAssetsExportService
   - ItemExportForMemberData
   - ItemExportForAdData
     - ItemExportForAdProductionData
     - ItemExportForAdStagingData

The following configuration options are supported:

| Group | Name | Data Type | Required | Multi-valued | Code Set | Default Value and Comments |
|---|---|---|---|---|---|---|
| General Info | ID (Autogenerated) | Number |  |  |  |  |
| General Info | Member ID (Autogenerated) | Number |  |  |  | {Buser.getSecurityContextValue} |
| General Info | Export Name | Text | Yes |  |  |  |
| General Info | Description | Text | Yes |  |  |  |
| General Info | Export Submitted By | Text | Yes |  |  |  |
| General Info | Export Type | Text | Yes |  | Export Type |  |
| General Info | Hierarchy | Text |  |  |  | Only applicable for AD exports; derived automatically for member exports |
| General Info | Use Legacy CX1 Headers | Text |  |  | Yes No | No - only applicable for Taxonomy Information export |
| Export Target | Export Target Type | Text | Yes |  | Export Target | File |
| Export Target | File Format | Text | Yes |  | File Format | COMMA |
| Export Target | Filename Prefix | Text |  |  |  |  |
| S/FTP | Protocol | Text | Yes |  | Protocol |  |
| S/FTP | S/FTP Hostname | Text | Yes |  |  |  |
| S/FTP | S/FTP Port | Number | Yes |  |  |  |
| S/FTP | S/FTP Path | Text | Yes |  |  |  |
| S/FTP | S/FTP Username | Text | Yes |  |  |  |
| S/FTP | S/FTP Password | Text | Yes |  |  |  |
| Email | Notification Email Addresses | Text |  | Yes |  |  |
| Record Filters | Export Language | Text |  |  |  | en |
| Record Filters | Special Character Handling | Text | Yes |  | Special Character Handling | UTF8 |
| Record Filters | Full/Delta | Text |  |  | Full Delta | Full |
| Record Filters | Saved Set or Saved Search | Text |  |  | Filter | No_Filter |
| Record Filters | Saved Set Name | Text |  |  |  |  |
| Record Filters | Saved Search Name | Text |  |  |  |  |
| Split Info | Maximum Number of Records per File | Text |  |  | Number of Rows Split |  |
| Split Info | Split by Attributes | Text |  | Yes | Split By Attributes |  |
| Global Attributes | Include Global Attributes | Text |  |  | Yes No |  |
| Global Attributes | Global Attributes Source | Text |  |  | Attributes Source (Merge Mbr   Override) |  |
| Category Attributes | Include Category Attributes | Text |  |  | Yes No | No |
| Category Attributes | Category Attributes Source | Text |  |  | Attributes Source (Merge Mbr   Override) |  |
| Category Attributes | Category Attributes Format | Text |  |  | Category Attributes Format | Attribute_Column_Triplets |
| Category Attributes | Concatenate Value and UOM | Text |  |  | Yes No | No |
| Category Attributes | Number of Category Attribute Columns | Text |  |  | Category Attribute Columns |  |
| Assets | Assets Source | Text |  |  | Attributes Source (Merge Combo) |  |
| Assets | Export SKU to Asset URL Map File | Text |  |  | Yes No | No |
| Assets | Export Unique Asset URL File | Text |  |  | Yes No | No |
| Assets | Export Assets | Text |  |  | Yes No | No |
| Assets | Asset Variants | Text |  | Yes | Asset Type |  |

Global attribute mapping is a list of global columns that are being requested as part of each export. The following configuration options are supported for each mapping:

| Name | Data Type | Is Required | Code Set and Comments |
|---|---|---|---|
| Column Sequence | Number | Yes |  |
| Display/Column Name | Text |  |  |
| Value Type | Text | Yes | Value Type - depending on this selection, one of the next three options will be required. |
| Static Value | Text |  |  |
| Attribute Name | Text |  | AttributeName |
| Special Global Column | Text |  | SpecialGlobalColumn |
| Multivalue Separator | Text |  |  |
| Value Prefix | Text |  |  |
| Value Suffix | Text |  |  |

### Special attribute columns

The Item Data and Digital Assets export for AD contains a configuration option where users (member or AD admin) can choose a special column that is derived from one or more attributes in one or more repositories:
 - Assets
 - Competitor
 - Features
 - Product
 - Taxonomy
 - Wholesaler

## Core processor components

These classes provide a set of core actions or services that can be configured and weaved together to extract data and transform it based on configuration options requested from the UI.

 - AddStaticColumns
 - AggregateRows
 - CoalesceColumns
 - CompressFiles
 - ConcatenateAttributes
 - DownloadAssets
 - HandleSpecialCharacters
 - JoinRecordsets
 - LookupCodesets
 - PivotToHeadersFromColumn
 - PivotToMultipleColumns
 - ReadFromTextFile
 - ReadItemsFromRepository
 - RenameColumns
 - SaveToFile
 - SendEmail
 - SendToFtp
 - SplitDataset
 - SpecialValueCalculator _(Interface)_ - see _Special attribute columns_ section above.

## Application classes

### Classes in exports-worker
 - Processor _(Abstract class)_
 - ExportService _(Abstract class)_
 - ExportWorkerApplication
 - MessageProcessor
 - JobMonitorService
 - SentenceGenerator _(no longer used)_
 - Constants
 - CategoryAttributeComparator

### Classes in exports-controller
 - ExportControllerApplication
 - MessageSender
 - ScheduleConfiguration
 - ScheduleTask

### Classes in exports-core
 - ApiService
 - ApplicationProperties
 - EnterworksRepository
 - ProcessorData
 - StringListAttributeConverter
 - Utilities

## Data classes

In addition to the above, there are _Entity_, _Repository_ and _Enumeration_ classes that represent database objects and JPA actions that can ben performed on them.

### Core data classes
 - AttributeSource
 - BCodeSetDetailEntity
 - BCodeSetEntity
 - BCodeSetLevelEntity
 - BCodeSetTypeEntity
 - BFormatAttrEntity
 - BGroupEntity
 - BGroupUserEntity
 - BJobAbortEntity
 - BJobEntity
 - BJobHistoryEntity
 - BLanguageEntity
 - BMasterRepositoryEntity
 - BMasterRepositoryItemEntity
 - BProfileEntity
 - BSavedSetEntity
 - BSavedSetItemEntity
 - BSavedSetRepoEntity
 - BUserEntity
 - CategoryAttributeColumns
 - CategoryAttributesFormat
 - CodeSetDetailRepository
 - CodeSetLevelRepository
 - CodeSetRepository
 - CodeSetRepositoryExtended
 - CodeSetRepositoryExtendedImpl
 - CodeSetTypeRepository
 - CommonDatabaseFunctionsRepository
 - CommonDatabaseFunctionsRepositoryImpl
 - ExportConfigurationEntity
 - ExportConfigurationRepository
 - ExportConfigurationRepositoryExtended
 - ExportConfigurationRepositoryExtendedImpl
 - ExportItemIds
 - ExportItemIdsRepository
 - ExportItemIdsRepositoryExtended
 - ExportItemIdsRepositoryExtendedImpl
 - ExportLogEntity
 - ExportLogRepository
 - ExportLogRepositoryExtended
 - ExportLogRepositoryExtendedImpl
 - ExportMappingEntity
 - ExportScheduleEntity
 - ExportScheduleRepository
 - ExportScheduleRepositoryExtended
 - ExportScheduleRepositoryExtendedImpl
 - ExportStatus
 - FileFormat
 - Filter
 - FormatAttrRepository
 - FtpProtocol
 - FullDelta
 - GroupRepository
 - GroupUserRepository
 - JobAbortRepository
 - JobHistoryRepository
 - JobRepository
 - LanguageRepository
 - MasterRepositoryItemRepository
 - MasterRepositoryItemRepositoryExtended
 - MasterRepositoryItemRepositoryExtendedImpl
 - MasterRepositoryRepository
 - MemberEntity
 - MemberRepository
 - ProfileRepository
 - ProfileRepositoryExtended
 - ProfileRepositoryExtendedImpl
 - SavedSetItemRepository
 - SavedSetRepoRepository
 - SavedSetRepository
 - ScheduleStatus
 - ScheduleType
 - SpecialCharacters
 - StringEntity
 - TargetType
 - UserRepository
 - ValueType
 - YesNo

### AD-specific data classes
 - AdOrMemberBasedEntityRepository
 - AssetLinkEntity
 - AssetLinkRepository
 - CategoryAttributeMetadataEntity
 - CategoryAttributeMetadataRepository
 - ClassificationEntity
 - ClassificationRepository
 - CompetitorEntity
 - CompetitorRepository
 - ManufacturerBrandEntity
 - ManufacturerBrandRepository
 - ProductEntity
 - ProductRepository
 - SchemaEntity
 - SchemaRepository
 - SkuAssets
 - TaxonomyEntity
 - TaxonomyRepository
 - WholesalerEntity
 - WholesalerRepository
