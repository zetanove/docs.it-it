---
title: "Elemento &lt;legacyCorruptedStateExceptionsPolicy&gt; | Microsoft Docs"
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
  - "<legacyCorruptedStateExceptionsPolicy> (elemento)"
  - "legacyCorruptedStateExceptionsPolicy (elemento)"
ms.assetid: e0a55ddc-bfa8-4f3e-ac14-d1fc3330e4bb
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Elemento &lt;legacyCorruptedStateExceptionsPolicy&gt;
Specifica se Common Language Runtime consente al codice gestito di rilevare violazioni di accesso e altre eccezioni di stato danneggiato.  
  
## Sintassi  
  
```  
<legacyCorruptedStateExceptionsPolicy enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica che l'applicazione rileverà le eccezioni di stato danneggiato, ad esempio le violazioni di accesso.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|L'applicazione non rileverà le eccezioni di stato danneggiato, ad esempio le violazioni di accesso.  Questa è l'impostazione predefinita.|  
|`true`|L'applicazione rileverà le eccezioni di stato danneggiato, ad esempio le violazioni di accesso.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 In .NET Framework 3.5 e versioni precedenti, Common Language Runtime consente al codice gestito di rilevare le eccezioni generate da stati di processo danneggiati.  Una violazione di accesso è un esempio di questo tipo di eccezione.  
  
 A partire da [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], il codice gestito non rileva più questo tipo di eccezioni nei blocchi `catch`.  Tuttavia, esistono due modi per eseguire l'override di questa modifica e mantenere la gestione delle eccezioni di stato danneggiato:  
  
-   Impostare l'attributo `enabled` dell'elemento `<legacyCorruptedStateExceptionsPolicy>` su `true`.  Questa impostazione di configurazione viene applicata all'intero processo e influisce su tutti i metodi.  
  
 In alternativa  
  
-   Applicare l'attributo <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=fullName> al metodo che contiene il blocco `catch` delle eccezioni.  
  
 Questo elemento di configurazione è disponibile solo in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] e versioni successive.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come specificare che l'applicazione deve ripristinare il comportamento delle versioni precedenti a [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] e rilevare tutte le eccezioni di stato danneggiato.  
  
```  
<configuration>  
   <runtime>  
      <legacyCorruptedStateExceptionsPolicy enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)