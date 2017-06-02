---
title: "Funzioni matematiche | Microsoft Docs"
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
ms.assetid: b040c7cb-156d-40f2-9152-61065b18148c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Funzioni matematiche
Il provider di dati .NET Framework per SQL Server \(SqlClient\) fornisce funzioni matematiche che eseguono calcoli in valori di input forniti come argomenti e restituiscono un risultato di tipo numerico.  Tali funzioni si trovano nello spazio dei nomi SqlServer, disponibile quando si usa SqlClient.  Una proprietà dello spazio dei nomi del provider consente a Entity Framework di individuare il prefisso usato dal provider per costrutti specifici, ad esempio tipi e funzioni. Nella tabella che segue sono illustrate le funzioni matematiche SqlClient.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|`ABS(` `expression` `)`|Esegue la funzione relativa al valore assoluto.<br /><br /> **Argomenti**<br /><br /> `expression`: `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valore restituito**<br /><br /> Valore assoluto dell'espressione specificata.<br /><br /> **Esempio**<br /><br /> `SqlServer.ABS(-2)`|  
|`ACOS(` `expression` `)`|Restituisce il valore dell'arcocoseno dell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.ACOS(.9)`|  
|`ASIN(` `expression` `)`|Restituisce il valore dell'arcoseno dell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.ASIN(.9)`|  
|`ATAN(` `expression` `)`|Restituisce il valore dell'arcotangente dell'espressione numerica specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.ATAN(9)`|  
|`ATN2(` `expression`, `expression``)`|Restituisce l'angolo, in radianti, la cui tangente è compresa tra le due espressioni numeriche specificate.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.ATN2(9, 8)`|  
|`CEILING(` `expression` `)`|Converte l'espressione specificata nel valore Integer più piccolo che è maggiore o uguale a tale espressione.<br /><br /> **Argomenti**<br /><br /> `expression`: `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valore restituito**<br /><br /> `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_CEILING](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_ceiling)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_CEILING](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_ceiling)]|  
|`COS(` `expression` `)`|Calcola il coseno trigonometrico dell'angolo specificato espresso in radianti.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.COS(45)`|  
|`COT(` `expression` `)`|Calcola la cotangente trigonometrica dell'angolo specificato espresso in radianti.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.COT(60)`|  
|`DEGREES(` `radians` `)`|Restituisce l'angolo corrispondente in gradi.<br /><br /> **Argomenti**<br /><br /> `expression`: `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valore restituito**<br /><br /> `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Esempio**<br /><br /> `SqlServer.DEGREES(3.1)`|  
|`EXP(` `expression` `)`|Calcola il valore esponenziale dell'espressione numerica specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.EXP(1)`|  
|`FLOOR(` `expression` `)`|Converte l'espressione specificata nel valore Integer più grande che risulta minore o uguale a tale espressione.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_FLOOR](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_floor)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_FLOOR](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_floor)]|  
|`LOG(` `expression` `)`|Calcola il logaritmo naturale dell'espressione `float` specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.LOG(100)`|  
|`LOG10(` `expression` `)`|Restituisce il logaritmo in base 10 dell'espressione `Double` specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.LOG10(100)`|  
|`PI()`|Restituisce il valore costante di pi greco sotto forma di oggetto `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.PI()`|  
|`POWER(` `numeric_expression, power_expression` `)`|Calcola il valore dell'espressione specificata elevato alla potenza indicata.<br /><br /> **Argomenti**<br /><br /> `numeric_expression`:  `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> `power_expression`: valore `Double` che rappresenta la potenza a cui elevare `numeric_expression`.<br /><br /> **Valore restituito**<br /><br /> Valore dell'oggetto `numeric_expression` specificato alla potenza `power_expression` indicata.<br /><br /> **Esempio**<br /><br /> `SqlServer.POWER(2,7)`|  
|`RADIANS(` `expression` `)`|Converte i gradi in radianti.<br /><br /> **Argomenti**<br /><br /> `expression`: `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valore restituito**<br /><br /> Un `Int32`, `Int64`,<br /><br /> `Double` o<br /><br /> `Decimal`.<br /><br /> **Esempio**<br /><br /> `SqlServer.RADIANS(360.0)`|  
|`RAND(`\[valore di inizializzazione\]`)`|Restituisce un valore casuale compreso tra 0 e 1.<br /><br /> **Argomenti**<br /><br /> Recupera il valore di inizializzazione come `Int32`.  Se non è specificato, il Motore di database di SQL Server assegna un valore di inizializzazione in modo casuale.  Per un valore di inizializzazione specificato, il risultato restituito è sempre lo stesso.<br /><br /> **Valore restituito**<br /><br /> Valore `Double` casuale compreso tra 0 e 1.<br /><br /> **Esempio**<br /><br /> `SqlServer.RAND()`|  
|`ROUND(` `numeric_expression, length` \[ ,`function` \]`)`|Restituisce un'espressione numerica, arrotondata alla precisione o alla lunghezza specificata.<br /><br /> **Argomenti**<br /><br /> `numeric_expression`:  `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> `length`: oggetto `Int32` che rappresenta la precisione a cui arrotondare `numeric_expression`.  Quando `length` è un numero positivo, l'oggetto `numeric_expression` viene arrotondato al numero di posizioni decimali specificato da `length`.  Quando `length` è un numero negativo, l'oggetto `numeric_expression` viene arrotondato a sinistra del separatore decimale, in base a quanto specificato da `length`.<br /><br /> `function`: `` \(facoltativo\) tipo `Int32` che rappresenta il tipo di operazione da eseguire.  Quando la funzione viene omessa oppure ha un valore 0 \(valore predefinito\), l'oggetto `numeric_expression` viene arrotondato.  Se viene specificato un valore diverso da 0, l'oggetto `numeric_expression` viene troncato.<br /><br /> **Valore restituito**<br /><br /> Valore dell'oggetto `numeric_expression` specificato alla potenza `power_expression` indicata.<br /><br /> **Esempio**<br /><br /> `SqlServer.ROUND(748.58, -3)`|  
|`SIGN(` `expression` `)`|Restituisce il segno positivo \(\+1\), zero \(0\) o il segno negativo \(\-1\) dell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: `Int32`, `Int64`, `Double` o `Decimal`<br /><br /> **Valore restituito**<br /><br /> `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Esempio**<br /><br /> `SqlServer.SIGN(-10)`|  
|`SIN(` `expression` `)`|Calcola il seno trigonometrico dell'angolo specificato, espresso in radianti, e restituisce un'espressione `Double`.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.SIN(20)`|  
|`SQRT(` `expression` `)`|Restituisce la radice quadrata dell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.SQRT(3600)`|  
|`SQUARE(` `expression` `)`|Restituisce la radice dell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: valore `Double`.<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> `SqlServer.SQUARE(25)`|  
|`TAN(` `expression` `)`|Calcola la tangente di un'espressione specificata.<br /><br /> **Argomenti**<br /><br /> `expression`: `Double`<br /><br /> **Valore restituito**<br /><br /> `Double`<br /><br /> **Esempio**<br /><br /> `SqlServer.TAN(45.0)`|  
  
 Per altre informazioni sulle funzioni matematiche supportate da SqlClient, vedere la documentazione relativa alla versione di SQL Server specificata nel file manifesto del provider SqlClient:  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[Funzioni matematiche \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115913)|[Funzioni matematiche \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115911)|[Funzioni matematiche \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115912)|  
  
## Vedere anche  
 [Funzioni di SqlClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)