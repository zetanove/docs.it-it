---
title: "Elemento &lt;disableFusionUpdatesFromADManager&gt; | Microsoft Docs"
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
  - "<disableFusionUpdatesFromADManager> (elemento)"
  - "disableFusionUpdatesFromADManager (elemento)"
ms.assetid: 58d2866c-37bd-4ffa-abaf-ff35926a2939
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;disableFusionUpdatesFromADManager&gt;
Specifica se il comportamento predefinito, ovvero consentire all'host di runtime di eseguire l'override delle impostazioni di configurazione di un dominio di applicazione, è disabilitato.  
  
## Sintassi  
  
```  
<disableFusionUpdatesFromADManager enabled="0|1"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|enabled|Attributo obbligatorio.<br /><br /> Specifica se l'opzione predefinita di eseguire l'override delle impostazioni Fusion è disabilitata.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|0|L'opzione di eseguire l'override delle impostazioni Fusion non è disabilitata.  Si tratta del comportamento predefinito, a partire da [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)].|  
|1|L'opzione di eseguire l'override delle impostazioni Fusion è disabilitata.  In questo modo è possibile ripristinare il comportamento delle versioni precedenti di .NET Framework.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 A partire da [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], il comportamento predefinito è consentire all'oggetto <xref:System.AppDomainManager> di eseguire l'override delle impostazioni di configurazione tramite la proprietà <xref:System.AppDomainSetup.ConfigurationFile%2A> o il metodo <xref:System.AppDomainSetup.SetConfigurationBytes%2A> dell'oggetto <xref:System.AppDomainSetup> passato all'implementazione del metodo <xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=fullName> nella sottoclasse di <xref:System.AppDomainManager>.  Per il dominio di applicazione predefinito, le impostazioni modificate eseguono l'override delle impostazioni specificate dal file di configurazione dell'applicazione.  Per gli altri domini di applicazione, tali impostazioni eseguono l'override delle impostazioni di configurazione passate al metodo <xref:System.AppDomainManager.CreateDomain%2A?displayProperty=fullName> o <xref:System.AppDomain.CreateDomain%2A?displayProperty=fullName>.  
  
 È possibile passare nuove informazioni di configurazione o passare null \(`Nothing` in Visual Basic\) per eliminare le informazioni di configurazione passate.  
  
 Non passare informazioni di configurazione sia alla proprietà <xref:System.AppDomainSetup.ConfigurationFile%2A> sia al metodo <xref:System.AppDomainSetup.SetConfigurationBytes%2A>.  Se si passano informazioni di configurazione a entrambi, le informazioni passate alla proprietà <xref:System.AppDomainSetup.ConfigurationFile%2A> vengono ignorate, poiché il metodo <xref:System.AppDomainSetup.SetConfigurationBytes%2A> esegue l'override delle informazioni di configurazione contenute nel file di configurazione dell'applicazione.  Se si utilizza la proprietà <xref:System.AppDomainSetup.ConfigurationFile%2A>, è possibile passare null \(`Nothing` in Visual Basic\) al metodo <xref:System.AppDomainSetup.SetConfigurationBytes%2A> per eliminare qualsiasi byte di configurazione specificato nella chiamata al metodo <xref:System.AppDomainManager.CreateDomain%2A?displayProperty=fullName> o <xref:System.AppDomain.CreateDomain%2A?displayProperty=fullName>.  
  
 Oltre alle informazioni di configurazione, è possibile modificare le impostazioni seguenti dell'oggetto <xref:System.AppDomainSetup> passato all'implementazione del metodo <xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=fullName>: <xref:System.AppDomainSetup.ApplicationBase%2A>, <xref:System.AppDomainSetup.ApplicationName%2A>, <xref:System.AppDomainSetup.CachePath%2A>, <xref:System.AppDomainSetup.DisallowApplicationBaseProbing%2A>, <xref:System.AppDomainSetup.DisallowBindingRedirects%2A>, <xref:System.AppDomainSetup.DisallowCodeDownload%2A>, <xref:System.AppDomainSetup.DisallowPublisherPolicy%2A>, <xref:System.AppDomainSetup.DynamicBase%2A>, <xref:System.AppDomainSetup.LoaderOptimization%2A>, <xref:System.AppDomainSetup.PrivateBinPath%2A>, <xref:System.AppDomainSetup.PrivateBinPathProbe%2A>, <xref:System.AppDomainSetup.ShadowCopyDirectories%2A> e <xref:System.AppDomainSetup.ShadowCopyFiles%2A>.  
  
 Come alternativa all'utilizzo dell'elemento `<disableFusionUpdatesFromADManager>` è possibile disabilitare il comportamento predefinito creando un'impostazione del Registro di sistema o impostando una variabile di ambiente.  Nel Registro di sistema, creare un valore DWORD denominato `COMPLUS_disableFusionUpdatesFromADManager` in `HKCU\Software\Microsoft\.NETFramework` o `HKLM\Software\Microsoft\.NETFramework` e impostarlo su 1.  Nella riga di comando, impostare la variabile di ambiente `COMPLUS_disableFusionUpdatesFromADManager` su 1.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come disabilitare l'opzione di eseguire l'override delle impostazioni Fusion tramite l'elemento `<disableFusionUpdatesFromADManager>`.  
  
```  
<configuration>  
   <runtime>  
      <disableFusionUpdatesFromADManager enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Come il runtime individua gli assembly](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)