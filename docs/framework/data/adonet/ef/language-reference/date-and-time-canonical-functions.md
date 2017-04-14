---
title: "Funzioni canoniche di data e ora | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 9628b74f-1585-436a-b385-8b02ed0cdd63
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Funzioni canoniche di data e ora
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] include funzioni canoniche di data e ora.  
  
## Note  
 Nella tabella seguente sono illustrate le funzioni canoniche [!INCLUDE[esql](../../../../../../includes/esql-md.md)] di data e ora. `datetime` è un valore <xref:System.DateTime>.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|`AddNanoseconds(` `expression`, `number``)`|Aggiunge i nanosecondi specificati dal valore di `number` all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime`, `DateTimeOffset` o `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddMicroseconds(` `expression`, `number``)`|Aggiunge il `number` specificato di microsecondi all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime`, `DateTimeOffset` o `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddMilliseconds(` `expression`, `number``)`|Aggiunge il `number` specificato di millisecondi all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime`, `DateTimeOffset` o `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddSeconds(` `expression`, `number``)`|Aggiunge il `number` specificato di secondi all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime`, `DateTimeOffset` o `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddMinutes(` `expression`, `number``)`|Aggiunge il `number` specificato di minuti all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime`, `DateTimeOffset` o `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddHours(` `expression`, `number``)`|Aggiunge il `number` specificato di ore all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime`, `DateTimeOffset` o `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddDays(` `expression`, `number``)`|Aggiunge il `number` specificato di giorni all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime` o `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddMonths(` `expression`, `number``)`|Aggiunge il `number` specificato di mesi all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime` o `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`AddYears(` `expression`, `number``)`|Aggiunge il `number` specificato di anni all'oggetto `expression`.<br /><br /> **Argomenti**<br /><br /> `expression`: `DateTime` o `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`CreateDateTime(` `year`, `month`, `day`, `hour`, `minute`, `second``)`|Restituisce un nuovo valore `DateTime` come data e ora correnti del server nel fuso orario del server.<br /><br /> **Argomenti**<br /><br /> `year`, `month`, `day`, `hour`, `minute`: `Int16` e `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `DateTime`.|  
|`CreateDateTimeOffset(` `year`, `month`, `day`, `hour`, `minute`, `second`, `tzoffset``)`|Restituisce un nuovo valore `DateTimeOffset` come data e ora correnti del server rispetto al fuso orario UTC.<br /><br /> **Argomenti**<br /><br /> `year`, `month`, `day`, `hour`, `minute`, `tzoffset`: `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `DateTimeOffset`.|  
|`CreateTime(` `hour`, `minute`, `second``)`|Restituisce un nuovo valore `Time` come ora corrente.<br /><br /> **Argomenti**<br /><br /> `hour` e `minute`: `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Time`.|  
|`CurrentDateTime()`|Restituisce un valore `DateTime` come data e ora correnti del server nel fuso orario del server.<br /><br /> **Valore restituito**<br /><br /> Oggetto `DateTime`.|  
|`CurrentDateTimeOffset()`|Restituisce la data, l'ora e l'offset correnti come `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `DateTimeOffset`.|  
|`CurrentUtcDateTime()`|Restituisce un valore <xref:System.DateTime> come data e ora correnti del server nel fuso orario UTS.<br /><br /> **Valore restituito**<br /><br /> Oggetto `DateTime`.|  
|`Day(` `expression` `)`|Restituisce la parte relativa al giorno di `expression` come tipo `Int32` compreso tra 1 e 31.<br /><br /> **Argomenti**<br /><br /> Tipi `DateTime` e `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 12.`<br /><br /> `Day(cast('03/12/1998' as DateTime))`|  
|`DayOfYear(` `expression` `)`|Restituisce la parte relativa al giorno di `expression` come `Int32` compreso tra 1 e 366, dove 366 viene restituito come l'ultimo giorno di un anno bisestile.<br /><br /> **Argomenti**<br /><br /> Tipo `DateTime` o `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffNanoseconds(` `startExpression`, `endExpression``)`|Restituisce la differenza in nanosecondi tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` o `Time`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffMilliseconds(` `startExpression`, `endExpression``)`|Restituisce la differenza in millisecondi tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` o `Time`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffMicroseconds(` `startExpression`, `endExpression``)`|Restituisce la differenza in microsecondi tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` o `Time`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffSeconds(` `startExpression`, `endExpression``)`|Restituisce la differenza in secondi tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` o `Time`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffMinutes(` `startExpression`, `endExpression``)`|Restituisce la differenza in minuti tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` o `Time`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffHours(` `startExpression`, `endExpression``)`|Restituisce la differenza in ore tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` o `Time`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffDays(` `startExpression`, `endExpression``)`|Restituisce la differenza in giorni tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime` o `DateTimeOffset`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffMonths(` `startExpression`, `endExpression``)`|Restituisce la differenza in mesi tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime` o `DateTimeOffset`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`DiffYears(` `startExpression`, `endExpression``)`|Restituisce la differenza in anni tra `startExpression` e `endExpression`.<br /><br /> **Argomenti**<br /><br /> `startExpression`, `endExpression`: `DateTime` o `DateTimeOffset`. **Note:**  `startExpression` e `endExpression` devono essere dello stesso tipo. <br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`GetTotalOffsetMinutes(` `datetimeoffset` `)`|Restituisce il numero di minuti di offset di `datetimeoffset` rispetto al fuso orario GMT.  Generalmente si tratta di un valore compreso tra \+780 e \-780 \(\+ o \- 13 ore\). **Note:**  Questa funzione è supportata solo in SQL Server 2008. <br /><br /> **Argomenti**<br /><br /> Oggetto `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`Hour (` `expression` `)`|Restituisce la parte relativa all'ora di `expression` come tipo `Int32` compreso tra 0 e 23.<br /><br /> **Argomenti**<br /><br /> Tipi `DateTime, Time` e `DateTimeOffset`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 22.`<br /><br /> `Hour(cast('22:35:5' as DateTime))`|  
|`Millisecond(` `expression` `)`|Restituisce la parte relativa ai millisecondi di `expression` come tipo `Int32` compreso tra 0 e 999.<br /><br /> **Argomenti**<br /><br /> Tipi `DateTime, Time` e `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.|  
|`Minute(` `expression` `)`|Restituisce la parte relativa ai minuti di `expression` come tipo `Int32` compreso tra 0 e 59.<br /><br /> **Argomenti**<br /><br /> Tipo `DateTime, Time` o `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 35`<br /><br /> `Minute(cast('22:35:5' as DateTime))`|  
|`Month` `(``expression``)`|Restituisce la parte relativa al mese di `expression` come tipo `Int32` compreso tra 1 e 12.<br /><br /> **Argomenti**<br /><br /> Tipo `DateTime` o `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 3.`<br /><br /> `Month(cast('03/12/1998' as DateTime))`|  
|`Second(` `expression` `)`|Restituisce la parte relativa ai secondi di `expression` come tipo `Int32` compreso tra 0 e 59.<br /><br /> **Argomenti**<br /><br /> Tipi `DateTime, Time` e `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 5`<br /><br /> `Second(cast('22:35:5' as DateTime))`|  
|`TruncateTime(` `expression` `)`|Restituisce `expression`, con i valori dell'ora troncati.<br /><br /> **Argomenti**<br /><br /> Tipo `DateTime` o `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.|  
|`Year(` `expression` `)`|Restituisce la parte relativa all'anno di `expression` come `YYYY` `Int32`.<br /><br /> **Argomenti**<br /><br /> Tipi `DateTime` e `DateTimeOffset`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 1998.`<br /><br /> `Year(cast('03/12/1998' as DateTime))`|  
  
 Queste funzioni restituiscono `null` se l'input è `null`.  
  
 Una funzionalità equivalente è disponibile nel provider gestito del client Microsoft SQL.  Per altre informazioni, vedere [Funzioni di SqlClient per Entity Framework](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md).  
  
## Vedere anche  
 [Funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)