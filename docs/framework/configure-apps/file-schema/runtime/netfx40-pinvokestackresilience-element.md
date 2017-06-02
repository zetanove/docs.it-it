---
title: "Elemento &lt;NetFx40_PInvokeStackResilience&gt; | Microsoft Docs"
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
  - "<NetFx40_PInvokeStackResilience> (elemento)"
  - "NetFx40_PInvokeStackResilience (elemento)"
ms.assetid: 39fb1588-72a4-4479-af74-0605233b68bd
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Elemento &lt;NetFx40_PInvokeStackResilience&gt;
Specifica se il runtime corregge automaticamente dichiarazioni platform invoke errate in fase di esecuzione, al costo di transizioni più lente tra codice gestito e non gestito.  
  
## Sintassi  
  
```  
<NetFx40_PInvokeStackResilience  enabled="1|0"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se il runtime rileva dichiarazioni platform invoke errate e automaticamente corregge in fase di esecuzione lo stack sulle piattaforme a 32 bit.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`0`|Il runtime utilizza l'architettura del marshalling di interoperabilità più veloce introdotta in [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], che non rileva e non corregge dichiarazioni platform invoke errate.  Questa è l'impostazione predefinita.|  
|`1`|Il runtime utilizza transizioni più lente che rilevano e correggono dichiarazioni platform invoke errate.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 Questo elemento consente di negoziare interoperabilità più veloce per effettuare il marshalling per l'elasticità della fase di esecuzione rispetto a dichiarazioni platform invoke errate.  
  
 Iniziando con [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], un'architettura del marshalling di interoperabilità semplificata fornisce un miglioramento nelle prestazioni significativo per le transizioni da codice gestito a codice non gestito.   In versioni precedenti di .NET Framework, il livello del marshalling ha rilevato dichiarazioni di platform invoke errate sulle piattaforme a 32 bit e ha automaticamente fissato lo stack.  La nuova architettura del marshalling elimina questo passaggio.  Di conseguenza, le transizioni sono molto veloci, ma una dichiarazione platform invoke errata può provocare un errore del programma.  
  
 Per facilitare il rilevamento di dichiarazioni errate durante lo sviluppo, l'esperienza di debug di Visual Studio è stata migliorata.  [PInvokeStackImbalance](../../../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md) gestito dal debug di assistente \(MDA\) notifica dichiarazioni platform invoke errate quando l'applicazione è in esecuzione con il debugger allegato.  
  
 Per indirizzare scenari in cui l'applicazione utilizza componenti che non è possibile ricompilare e che dispongono di dichiarazioni platform invoke errate, è possibile utilizzare l'elemento `NetFx40_PInvokeStackResilience`.  L'aggiunta di questo elemento al file di configurazione dell'applicazione con `enabled="1"` sceglie in una modalità di compatibilità con il comportamento di versioni precedenti di .NET Framework, al costo di transizioni più lente.  Assembly compilati rispetto a versioni precedenti di .NET Framework vengono scelti automaticamente in questa modalità di compatibilità e non hanno bisogno di questo elemento.  
  
## File di configurazione  
 L'elemento può essere utilizzato esclusivamente nel file di configurazione dell'applicazione.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come scegliere a fronte dell'aumentata flessibilità rispetto a dichiarazioni platform invoke errate per un'applicazione, al costo di transizioni più lente tra codice gestito e non gestito.  
  
```  
<configuration>  
   <runtime>  
      <NetFx40_PInvokeStackResilience enabled="1"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [pInvokeStackImbalance](../../../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md)