---
title: "Elemento &lt;CompatSortNLSVersion&gt; | Microsoft Docs"
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
  - "<CompatSortNLSVersion> (elemento)"
  - "CompatSortNLSVersion (elemento)"
ms.assetid: 782cc82e-83f7-404a-80b7-6d3061a8b6e3
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Elemento &lt;CompatSortNLSVersion&gt;
Specifica che nel runtime devono essere utilizzati ordinamenti legacy quando si eseguono confronti di stringhe.  
  
## Sintassi  
  
```  
<CompatSortNLSVersion    
   enabled="4096"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica l'ID delle impostazioni locali di cui deve essere utilizzato l'ordinamento.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|4096|ID impostazioni locali mediante il quale viene rappresentato un ordinamento alternativo.  In questo caso, 4096 rappresenta l'ordinamento di [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] e versioni precedenti.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 Dal momento che le operazioni di confronto tra stringhe, ordinamento e combinazione di maiuscole e minuscole eseguite dalla classe <xref:System.Globalization.CompareInfo?displayProperty=fullName> in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] sono conformi allo standard Unicode 5.1, i risultati dei metodi di confronto di stringhe quali <xref:System.String.Compare%28System.String%2CSystem.String%29?displayProperty=fullName> e <xref:System.String.LastIndexOf%28System.String%29?displayProperty=fullName> potrebbero differire dalle versioni precedenti di .NET Framework.  Se l'applicazione dipende dal comportamento legacy, è possibile ripristinare il confronto di stringhe e le regole di ordinamento utilizzati in [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] e nelle versioni precedenti includendo l'elemento `<CompatSortNLSVersion>` nel file di configurazione dell'applicazione.  
  
> [!IMPORTANT]
>  Per il ripristino del confronto di stringhe legacy e delle regole di ordinamento è necessaria inoltre la disponibilità della libreria di collegamento dinamico sort00001000.dll nel sistema locale.  
  
 È inoltre possibile utilizzare l'ordinamento delle stringhe legacy e le regole di confronto in un dominio dell'applicazione specifico passando la stringa "NetFx40\_Legacy20SortingBehavior" al metodo <xref:System.AppDomainSetup.SetCompatibilitySwitches%2A> quando si crea il dominio dell'applicazione.  
  
## Esempio  
 Nell'esempio seguente viene creata un'istanza di due oggetti <xref:System.String> e viene chiamato il metodo <xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=fullName> per confrontarle utilizzando le convenzioni delle impostazioni cultura correnti.  
  
 [!code-csharp[String.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/string.breakingchanges/cs/example1.cs#1)]
 [!code-vb[String.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/string.breakingchanges/vb/example1.vb#1)]  
  
 Quando si esegue l'esempio in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], viene visualizzato l'output seguente.  
  
```  
sta follows a in the sort order.  
```  
  
 Si tratta di un output completamente diverso da quello che viene visualizzato quando si esegue l'esempio in [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)].  
  
```  
sta equals a in the sort order.  
```  
  
 Tuttavia, se si aggiunge il file di configurazione seguente alla directory dell'esempio e successivamente si esegue l'esempio in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], l'output è identico a quello prodotto dall'esempio quando viene eseguito in [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)].  
  
```  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <CompatSortNLSVersion enabled="4096"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)