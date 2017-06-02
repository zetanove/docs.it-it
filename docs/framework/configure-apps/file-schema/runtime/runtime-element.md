---
title: "Elemento &lt;runtime&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#runtime"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<runtime> (elemento)"
  - "tag contenitore, <runtime> (elemento)"
  - "runtime (elemento)"
ms.assetid: 1eb2fae3-de4b-45b6-852f-517c39b751bd
caps.latest.revision: 70
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 62
---
# Elemento &lt;runtime&gt;
Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.  
  
## Sintassi  
  
```  
<runtime>  
</runtime>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<alwaysFlowImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/alwaysflowimpersonationpolicy-element.md)|Specifica che il flusso dell'identità Windows passa sempre attraverso punti asincroni, indipendentemente dal modo in cui è stata ottenuta la rappresentazione.|  
|[\<appDomainManagerAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)|Specifica l'assembly che fornisce il gestore del dominio di applicazione predefinito nel processo.|  
|[\<appDomainManagerType\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagertype-element.md)|Specifica il tipo che funge da gestore del dominio di applicazione predefinito.|  
|[\<appDomainResourceMonitoring\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)|Indica al runtime di raccogliere statistiche su tutti i domini di applicazione nel processo per la durata del processo.|  
|[\<assemblyBinding\>](../../../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)|Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.|  
|[\<bypassTrustedAppStrongNames\>](../../../../../docs/framework/configure-apps/file-schema/runtime/bypasstrustedappstrongnames-element.md)|Specifica se la verifica dei nomi sicuri per gli assembly attendibili deve essere ignorata.|  
|[\<CompatSortNLSVersion\>](../../../../../docs/framework/configure-apps/file-schema/runtime/compatsortnlsversion-element.md)|Specifica che nel runtime deve essere utilizzato il comportamento di ordinamento legacy quando si eseguono i confronti di stringhe.|  
|[\<developmentMode\>](../../../../../docs/framework/configure-apps/file-schema/runtime/developmentmode-element.md)|Specifica se nell'ambiente di esecuzione viene effettuata una ricerca degli assembly nelle directory definite dalla variabile di ambiente DEVPATH.|  
|[\<disableCachingBindingFailures\>](../../../../../docs/framework/configure-apps/file-schema/runtime/disablecachingbindingfailures-element.md)|Specifica se è disabilitata la memorizzazione nella cache degli errori di associazione, che in .NET Framework versione 2.0 è attivata per impostazione predefinita.|  
|[\<disableCommitThreadStack\>](../../../../../docs/framework/configure-apps/file-schema/runtime/disablecommitthreadstack-element.md)|Specifica se viene eseguito il commit dello stack di thread completo all'avvio di un thread.|  
|[\<disableFusionUpdatesFromADManager\>](../../../../../docs/framework/configure-apps/file-schema/runtime/disablefusionupdatesfromadmanager-element.md)|Specifica se il comportamento predefinito, ovvero consentire all'host di runtime di eseguire l'override delle impostazioni di configurazione di un dominio di applicazione, è disabilitato.|  
|[\<enforceFIPSPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/enforcefipspolicy-element.md)|Specifica se imporre un requisito di configurazione del computer per cui gli algoritmi di crittografia devono essere conformi agli standard FIPS \(Federal Information Processing Standards\).|  
|[\<etwEnable\>](../../../../../docs/framework/configure-apps/file-schema/runtime/etwenable-element.md)|Specifica se abilitare la traccia eventi per Windows \(ETW\) per gli eventi Common Language Runtime.|  
|[\<forcePerformanceCounterUniqueSharedMemoryReads\>](../../../../../docs/framework/configure-apps/file-schema/runtime/forceperformancecounteruniquesharedmemoryreads-element.md)|Indica se PerfCounter.dll utilizza l'impostazione del registro di sistema di CategoryOptions nell'applicazione .NET Framework versione 1.1 per determinare se caricare dati del contatore delle prestazioni dalla memoria condivisa specifica della categoria o dalla memoria globale.|  
|[\<gcAllowVeryLargeObjects\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md)|Sulle piattaforme a 64 bit, consente alle matrici che hanno dimensione totale maggiore di 2 GB \(GB\).|  
|[\<gcConcurrent\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md)|Specifica se in Common Language Runtime viene eseguita la procedura di Garbage Collection in modo concorrente.|  
|[\<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)|Specifica se la Garbage Collection supporta più gruppi di CPU.|  
|[\<gcServer\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md)|Specifica se in Common Language Runtime viene eseguita la Garbage Collection per server.|  
|[\<generatePublisherEvidence\>](../../../../../docs/framework/configure-apps/file-schema/runtime/generatepublisherevidence-element.md)|Specifica se in fase di esecuzione vengono utilizzati criteri di sicurezza dall'accesso di codice dell'editore.|  
|[\<legacyCorruptedStateExceptionsPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/legacycorruptedstateexceptionspolicy-element.md)|Specifica se il runtime consente al codice gestito di intercettare violazioni di accesso e altre eccezioni di stato danneggiato.|  
|[\<legacyImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md)|Specifica che il flusso dell'identità Windows non passa attraverso punti asincroni, indipendentemente dalle impostazioni di flusso per il contesto di esecuzione nel thread corrente.|  
|[\<loadFromRemoteSources\>](../../../../../docs/framework/configure-apps/file-schema/runtime/loadfromremotesources-element.md)|Specifica se gli assembly provenienti da origini remote vengono caricati come assembly con attendibilità totale.|  
|[\<NetFx40\_LegacySecurityPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md)|Specifica se il runtime utilizza criteri legacy di sicurezza dall'accesso di codice \(CAS, Code Access Security\).|  
|[\<NetFx40\_PInvokeStackResilience\>](../../../../../docs/framework/configure-apps/file-schema/runtime/netfx40-pinvokestackresilience-element.md)|Specifica se il runtime corregge automaticamente dichiarazioni platform invoke errate in fase di esecuzione, al costo di transizioni più lente tra codice gestito e non gestito.|  
|[\<NetFx45\_CultureAwareComparerGetHashCode\_LongStrings\>](../../../../../docs/framework/configure-apps/file-schema/runtime/netfx45-cultureawarecomparergethashcode-longstrings-element.md)|Specifica se il runtime utilizza una quantità di memoria fissa per calcolare i codici hash per il metodo <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName>.|  
|[\<PreferComInsteadOfRemoting\>](../../../../../docs/framework/configure-apps/file-schema/runtime/prefercominsteadofmanagedremoting-element.md)|Specifica che il runtime utilizzerà l'interoperabilità COM anziché i servizi remoti fra i limiti dei domini di applicazione.|  
|[\<relativeBindForResources\>](../../../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md)|Ottimizza le ricerche per gli assembly satellite.|  
|[\<shadowCopyVerifyByTimeStamp\>](../../../../../docs/framework/configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md)|Specifica se la copia shadow utilizza il comportamento di avvio predefinito introdotto in [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] o ripristina il comportamento di avvio di versioni precedenti di .NET Framework.|  
|[\<supportPortability\>](../../../../../docs/framework/configure-apps/file-schema/runtime/supportportability-element.md)|Specifica che un'applicazione può fare riferimento allo stesso assembly in due implementazioni diverse di .NET Framework, disabilitando il comportamento predefinito che tratta gli assembly come equivalenti allo scopo della portabilità dell'applicazione.|  
|[\<system.runtime.caching\>](../../../../../docs/framework/configure-apps/file-schema/runtime/system-runtime-caching-element-cache-settings.md)|Fornisce informazioni di configurazione per la cache oggetti in memoria predefinita.|  
|[\<Thread\_UseAllCpuGroups\>](../../../../../docs/framework/configure-apps/file-schema/runtime/thread-useallcpugroups-element.md)|Specifica se il runtime distribuisce thread gestiti in tutti i gruppi della CPU.|  
|[\<ThrowUnobservedTaskExceptions\>](../../../../../docs/framework/configure-apps/file-schema/runtime/throwunobservedtaskexceptions-element.md)|Specifica se le eccezioni non gestite di attività devono far terminare un processo in esecuzione.|  
|[\<TimeSpan\_LegacyFormatMode\>](../../../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md)|Specifica se il runtime utilizza la formattazione legacy per i valori <xref:System.TimeSpan>.|  
|[\<UseRandomizedStringHashAlgorithm\>](../../../../../docs/framework/configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md)|Specifica se il runtime calcola i codici hash per le stringhe in base al dominio dell'applicazione.|  
|[\<UseSmallInternalThreadStacks\>](../../../../../docs/framework/configure-apps/file-schema/runtime/usesmallinternalthreadstacks-element.md)|Richiede che il runtime utilizzi dimensioni di stack esplicite anziché la dimensione di stack predefinita quando crea determinati thread che utilizza internamente.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
  
## Note  
 In .NET Framework versione 2.0 le identità rappresentate attraversano i punti asincroni di un dominio applicazione.  In .NET Framework versione 2.0 è possibile attivare o disabilitare il flusso delle rappresentazioni attraverso i punti asincroni configurando correttamente l'elemento runtime nel file machine.config o nel file di configurazione dell'applicazione.  Per ASP.NET il flusso delle rappresentazioni può essere configurato nel file aspnet.config contenuto nella directory \<Windows Folder\>\\Microsoft.NET\\Framework\\vx.x.xxxx.  
  
 Per impostazione predefinita, in ASP.NET viene disabilitato il flusso delle rappresentazioni nel file aspnet.config utilizzando le seguenti impostazioni di configurazione:  
  
```  
configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
      <alwaysFlowImpersonationPolicy enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
 Se in ASP.NET si desidera attivare il flusso delle rappresentazioni, è necessario utilizzare in modo esplicito le seguenti impostazioni di configurazione:  
  
```  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="false"/>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
 Per ulteriori informazioni, vedere [Elemento \<legacyImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md) e [Elemento \<alwaysFlowImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/alwaysflowimpersonationpolicy-element.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come reindirizzare una versione dell'assembly in un'altra.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
             <bindingRedirect oldVersion="1.0.0.0"  
                              newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Reindirizzamento delle versioni di assembly](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)   
 [How to: Disable Concurrent Garbage Collection](http://msdn.microsoft.com/it-it/ba2c6c67-5778-497c-9fac-5f793b5500c7)