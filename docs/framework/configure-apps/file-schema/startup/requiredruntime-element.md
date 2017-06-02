---
title: "Elemento &lt;requiredRuntime&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#requiredRuntime"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/requiredRuntime"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<requiredRuntime> (elemento)"
  - "tag contenitore, <requiredRuntime> (elemento)"
  - "requiredRuntime (elemento)"
ms.assetid: 9fa1639e-beb8-43be-b7a4-12f7b229c34b
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;requiredRuntime&gt;
Specifica che l'applicazione supporta solo la versione 1.0 di Common Language Runtime \(CLR\).  
  
## Sintassi  
  
```  
  
   <requiredRuntime    
version="runtime version"  
safemode="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`version`|Attributo facoltativo.<br /><br /> Valore della stringa che specifica la versione di .NET Framework supportata dall'applicazione corrente.  Tale valore deve corrispondere al nome di directory presente nella directory radice di installazione di .NET Framework.  Il contenuto del valore String non viene analizzato.|  
|`safemode`|Attributo facoltativo.<br /><br /> Specifica se il codice di avvio dell'ambiente di esecuzione consente di effettuare una ricerca nel Registro di sistema per determinare la versione dell'ambiente di esecuzione.|  
  
## Attributo safemode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il codice di avvio di runtime esegue la ricerca nel Registro di sistema.  Rappresenta il valore predefinito.|  
|`true`|Il codice di avvio di runtime non esegue la ricerca nel Registro di sistema.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`startup`|Contiene l'elemento `<requiredRuntime>`.|  
  
## Note  
 Nelle applicazioni compilate per supportare esclusivamente la versione 1.0 del runtime è necessario utilizzare l'elemento `<requiredRuntime>`.  Nelle applicazioni compilate con la versione 1.1 o successive del runtime sarà necessario utilizzare l'elemento `<supportedRuntime>` .  
  
> [!NOTE]
>  Se si utilizza la funzione [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md) per specificare il file di configurazione, è necessario utilizzare l'elemento `<requiredRuntime>` per tutte le versioni del runtime.  L'elemento `<supportedRuntime>` viene ignorato quando si utilizza [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md).  
  
 La stringa dell'attributo `version` deve corrispondere al nome della cartella di installazione relativa alla versione di .NET Framework specificata.  Tale stringa non viene interpretata.  Se il codice di avvio dell'ambiente di esecuzione non individua una cartella corrispondente, l'ambiente di esecuzione non viene caricato; il codice di avvio visualizza un messaggio di errore e si interrompe.  
  
> [!NOTE]
>  Il codice di avvio per un'applicazione inclusa in Microsoft Internet Explorer ignora l'elemento `<requiredRuntime>`.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare la versione dell'ambiente di esecuzione in un file di configurazione.  
  
```  
<configuration>  
   <startup>  
      <requiredRuntime version="v1.0.3705" safemode="true"/>  
   </startup>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni di avvio](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<PaveOver\> Specifying Which Runtime Version to Use](http://msdn.microsoft.com/it-it/c376208d-980d-42b4-865b-fbe0d9cc97c2)