---
title: "Elemento &lt;TimeSpan_LegacyFormatMode&gt; | Microsoft Docs"
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
  - "<TimeSpan_LegacyFormatMode> (elemento)"
  - "TimeSpan_LegacyFormatMode (elemento)"
ms.assetid: 865e7207-d050-4442-b574-57ea29d5e2d6
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Elemento &lt;TimeSpan_LegacyFormatMode&gt;
Determina se il runtime mantiene un comportamento legacy in operazioni di formattazione con valori <xref:System.TimeSpan?displayProperty=fullName>.  
  
## Sintassi  
  
```  
<TimeSpan_LegacyFormatMode    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Consente di specificare se il runtime utilizza un comportamento di formattazione legacy con i valori <xref:System.TimeSpan?displayProperty=fullName>.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il runtime non ripristina il comportamento della formattazione legacy.|  
|`true`|Il runtime ripristina il comportamento della formattazione legacy.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 A partire da [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], la struttura <xref:System.TimeSpan?displayProperty=fullName>implementa l'interfaccia <xref:System.IFormattable>e supporta operazioni di formattazione con stringhe di formato standard e personalizzato.  Se un metodo dell'analisi incontra un identificatore di formato o una stringa di formato non supportati, genera un <xref:System.FormatException>.  
  
 In versioni precedenti di .NET Framework, la struttura <xref:System.TimeSpan> non ha implementato <xref:System.IFormattable> e non ha supportato stringhe di formato.  Tuttavia, molti sviluppatori ritengono erroneamente che <xref:System.TimeSpan> abbia supportato un set di stringhe di formato e le abbia utilizzate in [operazioni di formattazione composite](../../../../../docs/standard/base-types/composite-formatting.md) con metodi quali <xref:System.String.Format%2A?displayProperty=fullName>.  In genere, se un tipo implementa <xref:System.IFormattable> e supporta stringhe di formato, le chiamate ai metodi di formattazione con le stringhe di formato non supportate generano <xref:System.FormatException>.  Tuttavia, poiché <xref:System.TimeSpan> non ha implementato <xref:System.IFormattable>, il runtime ha ignorato la stringa di formato e ha invece chiamato il metodo <xref:System.TimeSpan.ToString?displayProperty=fullName>.  Significa che, anche se le stringhe di formato non hanno avuto effetto sull'operazione di formattazione, la loro presenza non ha provocato un <xref:System.FormatException>.  
  
 Per casi in cui il codice legacy passa un metodo di formattazione composita e una stringa del formato non valido e non è possibile ricompilare quel codice, è possibile utilizzare l'elemento`<TimeSpan_LegacyFormatMode>` per ripristinare il comportamento <xref:System.TimeSpan> legacy.  Quando si imposta l'attributo `enabled` di tale elemento su `true`, il metodo di formattazione composita provoca una chiamata a <xref:System.TimeSpan.ToString?displayProperty=fullName> piuttosto che a <xref:System.TimeSpan.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName>e <xref:System.FormatException> non viene generato.  
  
## Esempio  
 Nell'esempio seguente viene creata l'istanza di un oggetto <xref:System.TimeSpan> e si tenta di formattarlo con il metodo <xref:System.String.Format%28System.String%2CSystem.Object%29?displayProperty=fullName> tramite una stringa di formato standard non supportata.  
  
 [!code-csharp[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/timespan.breakingchanges/cs/legacyformatmode1.cs#1)]
 [!code-vb[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/timespan.breakingchanges/vb/legacyformatmode1.vb#1)]  
  
 Quando si esegue l'esempio su [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] o su una versione precedente, viene visualizzato l'output seguente:  
  
```  
12:30:45  
```  
  
 È notevolmente differente dall'output se si esegue l'esempio su [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] o versioni successive:  
  
```  
Invalid Format  
```  
  
 Tuttavia, se si aggiunge il file di configurazione seguente alla directory dell'esempio e successivamente si esegue l'esempio in [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] o versioni successive, l'output è identico a quello prodotto dall'esempio quando viene eseguito in [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)].  
  
```  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <TimeSpan_LegacyFormatMode enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)