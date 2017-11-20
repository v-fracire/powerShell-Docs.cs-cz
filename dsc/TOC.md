# [Přehled](overview.md)

## [Přehled platformy Desired State Configuration pro pracovníky s rozhodovací pravomocí](decisionMaker.md)

## [Přehled platformy Desired State Configuration pro techniky](DscForEngineers.md)

## [Rychlý start DSC](quickStart.md)

# [Konfigurace](configurations.md)

## [Přijetí konfigurace](enactingConfigurations.md)

## [Oddělení konfiguračních dat od dat prostředí](separatingEnvData.md)

## [Použití různých verzí prostředků](sxsResource.md)

## [Použití uživatelských přihlašovacích údajů ke spuštění DSC](runAsUser.md)

## [Určení závislostí mezi uzly](crossNodeDependencies.md)

## [Konfigurační data](configData.md)

### [Možnosti přihlašovacích údajů v konfiguračních datech](configDataCredentials.md)

## [Vnořování konfigurací](compositeConfigs.md)

## [Zabezpečení konfiguračního souboru MOF](secureMOF.md)

## [Částečné konfigurace](partialConfigs.md)

## [Psaní nápovědy ke konfiguracím DSC](configHelp.md)

## [Použití platformy DSC ke konfiguraci virtuálního počítače při prvním spuštění](bootstrapDsc.md)

### [Klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md)

# [Prostředky](resources.md)

## [Integrované prostředky](builtInResource.md)

### [Prostředek Archive](archiveResource.md)

### [Prostředek Environment](environmentResource.md)

### [Prostředek File](fileResource.md)

### [Prostředek Group](groupResource.md)

### [Prostředek GroupSet](groupSetResource.md)

### [Prostředek Log](logResource.md)

### [Prostředek Package](packageResource.md)

### [Prostředek ProcessSet](processSetResource.md)

### [Prostředek Registry](registryResource.md)

### [Prostředek Script](scriptResource.md)

### [Prostředek Service](serviceResource.md)

### [Prostředek ServiceSet](serviceSetResource.md)

### [Prostředek User](userResource.md)

### [Prostředek WaitForAll](waitForAllResource.md)

### [Prostředek WaitForAny](waitForAnyResource.md)

### [Prostředek WaitForSome](waitForSomeResource.md)

### [Prostředek WindowsFeature](windowsfeatureResource.md)

### [Prostředek WindowsFeatureSet](windowsFeatureSetResource.md)

### [Prostředek WindowsOptionalFeature](windowsOptionalFeatureResource.md)

### [Prostředek WindowsOptionalFeatureSet](windowsOptionalFeatureSetResource.md)

### [Prostředek WindowsPackageCab](windowsPackageCabResource.md)

### [Prostředek WindowsProcess](windowsProcessResource.md)

## [Tvorba vlastních prostředků](authoringResource.md) 

### [Vlastní prostředky založené na souboru MOF](authoringResourceMOF.md)

#### [Prostředek založený na souboru MOF v C#](authoringResourceMofCS.md)

### [Vlastní prostředky založené na třídě](authoringResourceClass.md)

### [Složené prostředky](authoringResourceComposite.md)

### [Psaní jednorázové instance prostředku DSC (doporučený postup)](singleInstance.md)

### [Kontrolní seznam při tvorbě prostředku](resourceAuthoringChecklist.md)

## [Ladění prostředků DSC](debugResource.md)

## [Přímé volání metod prostředku DSC](directCallResource.md)

# Local Configuration Manager

## [Konfigurace Local Configuration Manageru (LCM)](metaConfig.md)

## [Konfigurace LCM v PowerShellu 4.0](metaConfig4.md)

# Načítací model platformy DSC

## [Nastavení webového serveru vyžádané replikace](pullServer.md)

## [Nastavení serveru vyžádané replikace SMB pro DSC](pullServerSMB.md)

## [Nastavení načítacího klienta](pullClient.md)

### [Použití konfiguračních názvů k nastavení načítacího klienta](pullClientConfigNames.md)

### [Použití konfiguračních identifikátorů k nastavení načítacího klienta](pullClientConfigID.md)

## [Použití serveru sestav DSC](reportServer.md)

## [Osvědčené postupy serveru vyžádané replikace](secureServer.md)

# [Příklady DSC](dscExamples.md)

## [Vytvoření kanálu CI/CD prostřednictvím DSC, platformy Pester a služeb Visual Studio Team Services](dscCiCd.md)

## [Oddělení konfiguračních dat od dat prostředí](separatingEnvData.md)

# [Řešení potíží s DSC](troubleshooting.md)

# [Použití platformy DSC na Nano Serveru](nanoDsc.md)

# Platforma DSC na Linuxu

## [Začínáme s DSC pro Linux](lnxGettingStarted.md)

## [Integrované prostředky pro Linux](lnxBuiltInResources.md)

### [Prostředek nxArchive](lnxArchiveResource.md)

### [Prostředek nxEnvironment](lnxEnvironmentResource.md)

### [Prostředek nxFile](lnxFileResource.md)

### [Prostředek nxFileLine](lnxFileLineResource.md)

### [Prostředek nxGroup](lnxGroupResource.md)

### [Prostředek nxPackage](lnxPackageResource.md)

### [Prostředek nxService](lnxServiceResource.md)

### [Prostředek nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md)

### [Prostředek nxUser](lnxUserResource.md)

# [Použití platformy DSC v Microsoft Azure](azureDsc.md)

# Referenční informace o formátu MOF platformy DSC

## [Třída MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager.md)

### [Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-applyconfiguration.md)

### [Metoda DisableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)

### [Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)

### [Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getconfiguration.md)

### [Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)

### [Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)

### [Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)

### [Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)

### [Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-removeconfiguration.md)

### [Metoda ResourceGet třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-resourceget.md)

### [Metoda ResourceSet třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-resourceset.md)

### [Metoda ResourceTest třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-resourcetest.md)

### [Metoda RollBack třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-rollback.md)

### [Metoda SendConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendconfiguration.md)

### [Metoda SendConfigurationApply třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)

### [Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)

### [Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)

### [Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-stopconfiguration.md)

### [Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-testconfiguration.md)

# Další zdroje informací

## [Dokumenty white paper](whitepapers.md)
