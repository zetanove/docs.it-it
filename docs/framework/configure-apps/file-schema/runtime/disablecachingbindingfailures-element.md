---
title: "Elemento &lt;disableCachingBindingFailures&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCachingBindingFailures"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCachingBindingFailures"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<disableCachingBindingFailures> (elemento)"
  - "assembly [.NET Framework], memorizzazione nella cache di errori di associazione"
  - "memorizzazione nella cache di errori di associazione di assembly"
  - "disableCachingBindingFailures (elemento)"
ms.assetid: bf598873-83b7-48de-8955-00b0504fbad0
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Elemento &lt;disableCachingBindingFailures&gt;
Specifica se disabilitare la memorizzazione nella cache di errori di associazione degli assembly che si verificano perché l'assembly non è stato trovato tramite sondaggio.  
  
## Sintassi  
  
```  
<disableCachingBindingFailures enabled="0|1"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|enabled|Attributo obbligatorio.<br /><br /> Specifica se disabilitare la memorizzazione nella cache di errori di associazione degli assembly che si verificano perché l'assembly non è stato trovato tramite sondaggio.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|0|Non disabilita la memorizzazione nella cache degli errori di associazione degli assembly che si verificano perché l'assembly non è stato trovato tramite un sondaggio.  Si tratta del comportamento di associazione predefinito a partire da .NET Framework versione 2.0.|  
|1|Disabilita la memorizzazione nella cache di errori di associazione degli assembly che si verificano perché l'assembly non è stato trovato tramite sondaggio.  Questa impostazione ripristina il comportamento di associazione di .NET Framework versione 1.1.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 A partire da .NET Framework versione 2.0, il comportamento predefinito per il caricamento degli assembly consiste nel memorizzare nella cache tutti gli errori di associazione e di caricamento.  Se pertanto un tentativo di caricare un assembly ha esito negativo, le richieste successive di caricare lo stesso assembly verranno arrestate immediatamente, senza tentare di individuare l'assembly.  Questo elemento disabilita il comportamento predefinito relativo ad errori di associazione che si verificano perché l'assembly non è stato trovato nel percorso di sondaggio.  Questi errori generano <xref:System.IO.FileNotFoundException>.  
  
 Alcuni errori di associazione e caricamento non sono influenzati da tale elemento e vengono sempre memorizzati nella cache.  Questi errori si verificano perché l'assembly è stato trovato ma non è stato possibile caricarlo.  Generano <xref:System.BadImageFormatException> o <xref:System.IO.FileLoadException>.  Nell'elenco seguente sono inclusi alcuni esempi di tali errori.  
  
-   Se si tenta di caricare un file che non è un assembly valido, i tentativi successivi di caricare l'assembly non riusciranno anche se il file errato viene sostituito con l'assembly corretto.  
  
-   Se si tenta di caricare un assembly bloccato dal file system, i tentativi successivi di caricare l'assembly non riusciranno anche se l'assembly è stato rilasciato dal file system.  
  
-   Se una o più versioni dell'assembly che si sta tentando di caricare sono nel percorso di sondaggio ma la versione specifica necessaria non è fra loro, i successivi tentativi di caricamento della versione non riusciranno anche se la versione corretta viene spostata sul percorso del sondaggio.  
  
## Esempio  
 Nell'esempio di codice seguente viene mostrato come disabilitare la memorizzazione nella cache di errori di associazione degli assembly che si verificano perché l'assembly non è stato trovato tramite sondaggio.  
  
```  
<configuration>  
   <runtime>  
      <disableCachingBindingFailures enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Come il runtime individua gli assembly](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)