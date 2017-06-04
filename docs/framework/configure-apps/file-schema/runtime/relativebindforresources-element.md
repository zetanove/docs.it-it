---
title: "Elemento &lt;relativeBindForResources&gt; | Microsoft Docs"
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
  - "<relativeBindForResources> (elemento)"
  - "RelativeBindForResources (elemento)"
ms.assetid: 846ffa47-7257-4ce3-8cac-7ff627e0e34f
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;relativeBindForResources&gt;
Ottimizza le ricerche per gli assembly satellite.  
  
## Sintassi  
  
```vb  
<relativeBindForResources    
   enabled="true|false" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se Common Language Runtime ottimizza le ricerche per gli assembly satellite.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il runtime non ottimizza le ricerche per gli assembly satellite.  Rappresenta il valore predefinito.|  
|`true`|Il runtime ottimizza le ricerche per gli assembly satellite.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 In genere, Gestione Risorse ricerca le risorse, come documentato nell'argomento [Creazione del pacchetto e distribuzione delle risorse](../../../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  Ciò significa che quando Gestione Risorse cerca una particolare versione localizzata di una risorsa, potrebbe cercare nella Global Assembly Cache, cercare in una cartella con delle impostazioni cultura specifiche nella codebase dell'applicazione, eseguire una query su Windows Installer per gli assembly satellite e generare l'evento di <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>.  L'elemento `<relativeBindForResources>` ottimizza la modalità in cui Gestione Risorse ricerca negli assembly satellite.  Può migliorare le prestazioni durante la ricerca delle risorse nei seguenti casi:  
  
-   Quando l'assembly satellite viene distribuito nella stessa posizione dell'assembly di codice.  Ovvero se l'assembly di codice viene installato nella Global Assembly Cache, gli assembly satellite devono essere installati su di essa.  Se l'assembly di codice viene installato nel codebase dell'applicazione, gli assembly satellite devono essere installati in una cartella con delle impostazioni cultura specifiche nel codebase.  
  
-   Quando Windows Installer non viene utilizzato o viene utilizzato raramente per installazioni su richiesta di assembly satellite.  
  
-   Quando il codice dell'applicazione non gestisce l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>.  
  
 Impostare l'attributo `enabled` dell'elemento `<relativeBindForResources>` a `true` ottimizza la ricerca di Gestione risorse per gli assembly satellite come segue:  
  
-   Utilizza la posizione del codice assembly padre per ricercare l'assembly satellite.  
  
-   Non eseguire una query su Windows Installer per gli assembly satellite.  
  
-   Non viene generato l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>.  
  
## Vedere anche  
 [Creazione del pacchetto e distribuzione delle risorse](../../../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)