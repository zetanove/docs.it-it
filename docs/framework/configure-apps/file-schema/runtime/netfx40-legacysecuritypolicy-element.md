---
title: "Elemento &lt;NetFx40_LegacySecurityPolicy&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<NetFx40_LegacySecurityPolicy> (elemento)"
  - "NetFx40_LegacySecurityPolicy (elemento)"
ms.assetid: 07132b9c-4a72-4710-99d7-e702405e02d4
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Elemento &lt;NetFx40_LegacySecurityPolicy&gt;
Specifica se il runtime utilizza criteri legacy di sicurezza dall'accesso di codice \(CAS, Code Access Security\).  
  
## Sintassi  
  
```  
<NetFx40_LegacySecurityPolicy  
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se in fase di esecuzione vengono utilizzati criteri di sicurezza per l'accesso al codice legacy.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il runtime non utilizza criteri CAS legacy.  Questa è l'impostazione predefinita.|  
|`true`|Il runtime utilizza criteri CAS legacy.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 In .NET Framework 3.5 e versioni precedenti, i criteri CAS sono sempre abilitati.  In [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], i criteri CAS devono essere abilitati.  
  
 I criteri CAS sono specifici della versione.  I criteri CAS personalizzati presenti nelle versioni precedenti di .NET Framework devono essere specificati nuovamente in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)].  
  
 L'applicazione dell'elemento `<NetFx40_LegacySecurityPolicy>` a un assembly [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] non influisce sul [codice SecurityTransparent](../../../../../docs/framework/misc/security-transparent-code.md). Tuttavia, le regole di trasparenza vengono comunque applicate.  
  
> [!IMPORTANT]
>  L'applicazione dell'elemento `<NetFx40_LegacySecurityPolicy>` può dare luogo a riduzioni significative delle prestazioni per gli assembly di immagini native creati dal [Generatore di immagini native \(Ngen.exe\)](../../../../../docs/framework/tools/ngen-exe-native-image-generator.md) che non sono installati in [Global Assembly Cache](../../../../../docs/framework/app-domains/gac.md).  La riduzione delle prestazioni è causata dall'impossibilità del runtime di caricare gli assembly come immagini native quando l'attributo viene applicato, il che ne comporta il caricamento come assembly Just\-In\-Time.  
  
> [!NOTE]
>  Se si specifica una versione di .NET Framework di destinazione precedente a [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] nelle impostazioni del progetto di Visual Studio, i criteri di protezione dall'accesso di codice verranno abilitati, compresi i criteri di protezione dall'accesso di codice personalizzati specificati per tale versione.  Non sarà tuttavia possibile utilizzare i nuovi tipi e membri di [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)].  È inoltre possibile specificare una versione precedente di .NET Framework tramite l'[elemento \<supportedRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) nello schema delle impostazioni di avvio nel [file di configurazione dell'applicazione](../../../../../docs/framework/configure-apps/index.md).  
  
> [!NOTE]
>  Nella sintassi dei file di configurazione viene fatta distinzione tra maiuscole e minuscole.  È necessario utilizzare la sintassi fornita nelle sezioni Sintassi ed Esempio.  
  
## File di configurazione  
 L'elemento può essere utilizzato esclusivamente nel file di configurazione dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come attivare i criteri di sicurezza per l'accesso al codice legacy per un'applicazione.  
  
```  
<configuration>  
   <runtime>  
      <NetFx40_LegacySecurityPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)