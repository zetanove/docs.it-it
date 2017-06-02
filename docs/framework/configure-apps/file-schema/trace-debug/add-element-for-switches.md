---
title: "Elemento &lt;add&gt; per &lt;switches&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/switches/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento) per <switches>"
  - "add (elemento) per <switches>"
ms.assetid: 712ac3a7-7abf-4a9e-8db4-acd241c2f369
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Elemento &lt;add&gt; per &lt;switches&gt;
Consente di specificare il livello in cui viene impostata un'opzione di traccia.  
  
## Sintassi  
  
```  
<add name="switch name"  
     value="value"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|**name**|Attributo obbligatorio.<br /><br /> Specifica il nome dell'opzione.  Il valore di questo attributo corrisponde al parametro *displayName* passato al costruttore di opzioni.|  
|**predefinito**|Attributo obbligatorio.<br /><br /> Specifica il livello dell'opzione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`switches`|Contiene opzioni di traccia e il livello in cui vengono impostate.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
  
## Note  
 È possibile modificare il livello di un'opzione di traccia inserendola in un file di configurazione.  Se si tratta di un'opzione <xref:System.Diagnostics.BooleanSwitch>, è possibile attivarla e disattivarla.  Se si tratta, invece, di un'opzione <xref:System.Diagnostics.TraceSwitch>, è possibile assegnarle livelli differenti per specificare i tipi di messaggi di traccia o di debug generati dall'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento **\<add\>** per impostare l'opzione di traccia `General` sul livello [TraceLevel.Error](frlrfSystemDiagnosticsTraceLevelClassTopic) e come attivare l'opzione di traccia di tipo Boolean `Data`.  
  
```  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
         <add name="Data" value="1" />  
      </switches>  
   </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.Switch>   
 <xref:System.Diagnostics.TraceSwitch>   
 <xref:System.Diagnostics.BooleanSwitch>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)