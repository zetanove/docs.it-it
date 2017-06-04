---
title: "dateTimeInvalidLocalFormat MDA | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
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
  - "dates [.NET Framework], formatting"
  - "invalid date time local format"
  - "invalid local formats"
  - "MDAs (managed debugging assistants), invalid local formats"
  - "managed debugging assistants (MDAs), invalid local formats"
  - "dateTimeInvalidLocalFormat MDA"
  - "date formatting"
  - "time formatting"
  - "UTC formatting"
ms.assetid: c4a942bb-2651-4b65-8718-809f892a0659
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# dateTimeInvalidLocalFormat MDA
L'assistente al debug gestito `dateTimeInvalidLocalFormat` viene attivato quando per un'istanza di <xref:System.DateTime> archiviata in formato UTC \(Universal Coordinated Time\) viene utilizzato un formato riservato alle istanze locali di <xref:System.DateTime>.  Questo assistente non viene attivato per le istanze di <xref:System.DateTime> non specificate o predefinite.  
  
## Sintomi  
 Un'applicazione sta serializzando manualmente un'istanza di <xref:System.DateTime> in formato UTC utilizzando un formato locale:  
  
```  
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("yyyy-MM-dd'T'HH:mm:ss.fffffffzzz"));  
```  
  
### Causa  
 Il formato 'z' del metodo <xref:System.DateTime.ToString%2A?displayProperty=fullName> include l'offset del fuso orario locale, ad esempio "\+10:00" per l'ora di Sydney.  Di conseguenza, verrà generato un risultato significativo solo se il valore di <xref:System.DateTime> è locale.  Se il valore è in formato UTC, <xref:System.DateTime.ToString%2A?displayProperty=fullName> include l'offset del fuso orario locale, ma non visualizza né modifica l'identificatore del fuso orario.  
  
### Risoluzione  
 Le istanze di <xref:System.DateTime> in formato UTC devono essere formattate in modo che vengano identificate come UTC.  Per indicare un'ora in formato UTC si consiglia di utilizzare una 'Z':  
  
```  
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("yyyy-MM-dd'T'HH:mm:ss.fffffffZ"));  
```  
  
 Esiste inoltre un formato "o" che serializza un'istanza di <xref:System.DateTime> utilizzando la proprietà <xref:System.DateTime.Kind%2A>, che viene serializzata correttamente indipendentemente dal fatto che l'istanza sia in formato locale, UTC o non specificato:  
  
```  
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("o"));  
```  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non ha alcun effetto su Common Language Runtime.  
  
## Output  
 L'attivazione di questo assistente al debug gestito non genera alcun output specifico. È possibile, tuttavia, utilizzare lo stack di chiamate per determinare la posizione della chiamata <xref:System.DateTime.ToString%2A> che ha attivato l'assistente.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <dateTimeInvalidLocalFormat />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Si supponga ad esempio un'applicazione che sta serializzando indirettamente un valore <xref:System.DateTime> UTC utilizzando la classe <xref:System.Xml.XmlConvert> o <xref:System.Data.DataSet>, come descritto di seguito.  
  
```  
DateTime myDateTime = DateTime.UtcNow;  
String serialized = XMLConvert.ToString(myDateTime);  
```  
  
 Per impostazione predefinita, <xref:System.Xml.XmlConvert> e <xref:System.Data.DataSet> utilizzano formati locali per la serializzazione.  Per serializzare altri tipi di valori <xref:System.DateTime>, ad esempio UTC, sono necessarie opzioni aggiuntive.  
  
 Per questo esempio specifico, passare `XmlDateTimeSerializationMode.RoundtripKind` alla chiamata `ToString` su `XmlConvert`.  In questo modo i dati vengono serializzati come ora UTC.  
  
 Se si utilizza <xref:System.Data.DataSet>, impostare la proprietà <xref:System.Data.DataColumn.DateTimeMode%2A> nell'oggetto <xref:System.Data.DataColumn> su <xref:System.Data.DataSetDateTime>.  
  
```  
DateTime myDateTime = DateTime.UtcNow;  
String serialized = XmlConvert.ToString(myDateTime,   
    XmlDateTimeSerializationMode.RoundtripKind);  
```  
  
## Vedere anche  
 <xref:System.Globalization.DateTimeFormatInfo>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)