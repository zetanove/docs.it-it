---
title: "Elemento &lt;gcAllowVeryLargeObjects&gt; | Microsoft Docs"
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
  - "<gcAllowVeryLargeObjects> (elemento)"
  - "gcAllowVeryLargeObjects (elemento)"
ms.assetid: 5c7ea24a-39ac-4e5f-83b7-b9f9a1b556ab
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Elemento &lt;gcAllowVeryLargeObjects&gt;
Sulle piattaforme a 64 bit, consente alle matrici che hanno dimensione totale maggiore di 2 GB \(GB\).  
  
## Sintassi  
  
```  
<gcAllowVeryLargeObjects    
   enabled="true|false" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se gli array più grandi di 2 GB nella dimensione totale sono abilitati sulle piattaforme a 64 bit.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Gli array più grandi di 2 GB nella dimensione totale non sono abilitati.  Questa è l'impostazione predefinita.|  
|`true`|Gli array più grandi di 2 GB nella dimensione totale sono abilitati sulle piattaforme a 64 bit.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 Utilizzare questo elemento nel file di configurazione dell'applicazione abilita gli array con una dimensione maggiore di 2 GB, ma non modifica gli altri limiti sulla dimensione dell'oggetto o sulla dimensione degli array:  
  
-   Il numero massimo di elementi in un array è <xref:System.UInt32.MaxValue?displayProperty=fullName>.  
  
-   L'indice massimo di ogni singola dimensione è 2.147.483.591 \(0x7FFFFFC7\) per gli array di byte e gli array di strutture a byte singolo e 2.146.435.071 \(0X7FEFFFFF\) per gli altri tipi.  
  
-   La dimensione massima consentita per stringhe e altri oggetti che non siano array resterà invariata.  
  
> [!CAUTION]
>  Prima di abilitare questa funzionalità, assicurarsi che l'applicazione non includa codice unsafe che supponga che tutti gli array abbiano dimensioni minori di 2 GB.  Ad esempio, il codice unsafe che utilizza gli array come buffer può essere soggetto a sovraccarichi del buffer se viene scritto partendo dal presupposto che gli array non superino i 2 GB.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come attivare questa funzionalità per un'applicazione.  
  
```  
<configuration>  
  <runtime>  
    <gcAllowVeryLargeObjects enabled="true" />  
  </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)