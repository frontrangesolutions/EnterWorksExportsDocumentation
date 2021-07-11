# Export types and classes

The java project for *export-worker* is designed to be a set of classes called *processors* that perform specific tasks (like CompressFiles, ReadItemsFromRepository, etc), and a set of classes called *export services* that use the processors with specific parameters in a specific order depending on the configuration designed by the users in the UI.

## Export types built for AD

The following export types are built specifically for Affiliated Distributors

 - **CategoryAttributeMetadataExportService:**

 - **CompetitorInformationExportService:**

 - **HierarchyDefinitionExportService:**

 - **ItemDataAndDigitalAssetsExportService:**

   - **ItemExportForAdData:**

     - **ItemExportForAdProductionData:**

     - **ItemExportForAdStagingData:**

   - **ItemExportForMemberData:**

 - **ManufacturerBrandExportService:**

 - **MemberHierarchyExportService:**

 - **ProductInformationExportService:**

 - **TaxonomyExportService:**

 - **TestExportService:**

 - **WholesalerInformationExportService:**

### Special attribute columns

The Item Data and Digital Assets export for AD contains a configuration option where users (member or AD admin) can choose a special column that is derived from one or more attributes in one or more repositories:

 - **SpecialValueCalculatorForAssets:**

 - **SpecialValueCalculatorForCompetitor:**

 - **SpecialValueCalculatorForFeatures:**

 - **SpecialValueCalculatorForProduct:**

 - **SpecialValueCalculatorForTaxonomy:**

 - **SpecialValueCalculatorForWholesaler:**

## Core processor components

 - **AddStaticColumns:**

 - **AggregateRows:**

 - **CoalesceColumns:**

 - **CompressFiles:**

 - **ConcatenateAttributes:**

 - **DownloadAssets:**

 - **HandleSpecialCharacters:**

 - **JoinRecordsets:**

 - **LookupCodesets:**

 - **PivotToHeadersFromColumn:**

 - **PivotToMultipleColumns:**

 - **ReadFromTextFile:**

 - **ReadItemsFromRepository:**

 - **RenameColumns:**

 - **SaveToFile:**

 - **SendEmail:**

 - **SendToFtp:**

 - **SpecialValueCalculator:** _Interface_

 - **SplitDataset:**

## Application classes

### Classes in exports-worker

 - **ExportWorkerApplication:**

 - **MessageProcessor:**

 - **ExportService:** _Abstract class_

 - **JobMonitorService:**

 - **Processor:** _Abstract class_

 - **SentenceGenerator:**

 - **Constants:**

 - **CategoryAttributeComparator:**

### Classes in exports-controller

 - **ExportControllerApplication:**

 - **MessageSender:**

 - **ScheduleConfiguration:**

 - **ScheduleTask:**

### Classes in exports-core

 - **ApiService:**

 - **ApplicationProperties:**

 - **EnterworksRepository:**

 - **ProcessorData:**

 - **StringListAttributeConverter:**

 - **Utilities:**

## Data classes

In addition to the above, there are _Entity_, _Repository_ and _Enumeration_ classes that represent database objects and JPA actions that can ben performed on them.

### Core data classes

 - **AttributeSource:**

 - **BCodeSetDetailEntity:**

 - **BCodeSetEntity:**

 - **BCodeSetLevelEntity:**

 - **BCodeSetTypeEntity:**

 - **BFormatAttrEntity:**

 - **BGroupEntity:**

 - **BGroupUserEntity:**

 - **BJobAbortEntity:**

 - **BJobEntity:**

 - **BJobHistoryEntity:**

 - **BLanguageEntity:**

 - **BMasterRepositoryEntity:**

 - **BMasterRepositoryItemEntity:**

 - **BProfileEntity:**

 - **BSavedSetEntity:**

 - **BSavedSetItemEntity:**

 - **BSavedSetRepoEntity:**

 - **BUserEntity:**

 - **CategoryAttributeColumns:**

 - **CategoryAttributesFormat:**

 - **CodeSetDetailRepository:**

 - **CodeSetLevelRepository:**

 - **CodeSetRepository:**

 - **CodeSetRepositoryExtended:**

 - **CodeSetRepositoryExtendedImpl:**

 - **CodeSetTypeRepository:**

 - **CommonDatabaseFunctionsRepository:**

 - **CommonDatabaseFunctionsRepositoryImpl:**

 - **ExportConfigurationEntity:**

 - **ExportConfigurationRepository:**

 - **ExportConfigurationRepositoryExtended:**

 - **ExportConfigurationRepositoryExtendedImpl:**

 - **ExportItemIds:**

 - **ExportItemIdsRepository:**

 - **ExportItemIdsRepositoryExtended:**

 - **ExportItemIdsRepositoryExtendedImpl:**

 - **ExportLogEntity:**

 - **ExportLogRepository:**

 - **ExportLogRepositoryExtended:**

 - **ExportLogRepositoryExtendedImpl:**

 - **ExportMappingEntity:**

 - **ExportScheduleEntity:**

 - **ExportScheduleRepository:**

 - **ExportScheduleRepositoryExtended:**

 - **ExportScheduleRepositoryExtendedImpl:**

 - **ExportStatus:**

 - **FileFormat:**

 - **Filter:**

 - **FormatAttrRepository:**

 - **FtpProtocol:**

 - **FullDelta:**

 - **GroupRepository:**

 - **GroupUserRepository:**

 - **JobAbortRepository:**

 - **JobHistoryRepository:**

 - **JobRepository:**

 - **LanguageRepository:**

 - **MasterRepositoryItemRepository:**

 - **MasterRepositoryItemRepositoryExtended:**

 - **MasterRepositoryItemRepositoryExtendedImpl:**

 - **MasterRepositoryRepository:**

 - **MemberEntity:**

 - **MemberRepository:**

 - **ProfileRepository:**

 - **ProfileRepositoryExtended:**

 - **ProfileRepositoryExtendedImpl:**

 - **SavedSetItemRepository:**

 - **SavedSetRepoRepository:**

 - **SavedSetRepository:**

 - **ScheduleStatus:**

 - **ScheduleType:**

 - **SpecialCharacters:**

 - **StringEntity:**

 - **TargetType:**

 - **UserRepository:**

 - **ValueType:**

 - **YesNo:**

### AD-specific data classes

 - **AdOrMemberBasedEntityRepository:**

 - **AssetLinkEntity:**

 - **AssetLinkRepository:**

 - **CategoryAttributeMetadataEntity:**

 - **CategoryAttributeMetadataRepository:**

 - **ClassificationEntity:**

 - **ClassificationRepository:**

 - **CompetitorEntity:**

 - **CompetitorRepository:**

 - **ManufacturerBrandEntity:**

 - **ManufacturerBrandRepository:**

 - **ProductEntity:**

 - **ProductRepository:**

 - **SchemaEntity:**

 - **SchemaRepository:**

 - **SkuAssets:**

 - **TaxonomyEntity:**

 - **TaxonomyRepository:**

 - **WholesalerEntity:**

 - **WholesalerRepository:**
