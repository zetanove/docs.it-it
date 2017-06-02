---
title: "Elemento &lt;assert&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/assert"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#assert"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<assert> (elemento)"
  - "assert (elemento)"
ms.assetid: ef4c3229-b151-4d85-8091-e6456af9b935
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Elemento &lt;assert&gt;
Consente di specificare se deve essere visualizzata una finestra di messaggio quando viene richiamato il metodo <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> e permette, inoltre, di specificare il nome del file in cui scrivere i messaggi.  
  
## Sintassi  
  
```  
  
<assert assertuienabled="true|false" logfilename="file name"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`assertuienabled`|Attributo facoltativo.<br /><br /> Specifica se deve essere visualizzata una finestra di messaggio quando il metodo **Debug.Assert** restituisce **false**.|  
|`logfilename`|Attributo facoltativo.<br /><br /> Specifica il nome del file in cui scrivere il messaggio se **Debug.Assert** restituisce **false**.|  
  
## Attributo assertuienabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`true`|La finestra di messaggio viene visualizzata.  Questa è l'impostazione predefinita.|  
|`false`|La finestra di messaggio non viene visualizzata.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
  
## Note  
 Entrambi gli attributi dell'elemento **\<assert\>** sono facoltativi.  È possibile disabilitare le finestre di messaggio senza specificare un file in cui scrivere i messaggi oppure specificare tale file lasciando attivate le finestre di messaggio.  
  
## Esempio  
 Nell'esempio riportato di seguito viene mostrato come disabilitare la visualizzazione di finestre di messaggio quando viene richiamato il metodo **Debug.Assert** e vengono scritti i messaggi in `c:\log.txt`.  
  
```  
<configuration>  
   <system.diagnostics>  
      <assert assertuienabled="false" logfilename="c:\log.txt"/>  
   </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.Debug>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)