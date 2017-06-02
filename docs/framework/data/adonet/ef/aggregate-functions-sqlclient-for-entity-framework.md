---
title: "Funzioni di aggregazione (SqlClient per Entity Framework) | Microsoft Docs"
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
ms.assetid: 03303f01-b591-4efc-9875-f9c608edff0b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Funzioni di aggregazione (SqlClient per Entity Framework)
Il provider di dati .NET Framework per SQL Server \(SqlClient\) fornisce funzioni di aggregazione  che eseguono calcoli su un set di valori di input e restituiscono un valore.  Tali funzioni si trovano nello spazio dei nomi SqlServer, disponibile quando si usa SqlClient.  Una proprietà dello spazio dei nomi del provider consente a Entity Framework di individuare il prefisso usato dal provider per costrutti specifici, ad esempio tipi e funzioni.  
  
 Nella tabella seguente sono riportate le funzioni di aggregazione di SqlClient:  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|`AVG(` `expression` `)`|Restituisce la media dei valori di una raccolta.<br /><br /> I valori Null vengono ignorati.<br /><br /> **Argomenti**<br /><br /> Valore `Int32`, `Int64`, `Double` e `Decimal`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_AVG](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_avg)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_AVG](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_avg)]|  
|`CHECKSUM_AGG(` `collection` `)`|Restituisce il checksum dei valori in una raccolta.<br /><br /> I valori Null vengono ignorati.<br /><br /> **Argomenti**<br /><br /> Raccolta \(`Int32`\).<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_CHECKSUM](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_checksum)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_CHECKSUM](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_checksum)]|  
|`COUNT(` `expression` `)`|Restituisce il numero di elementi in una raccolta come un valore `Int32`.<br /><br /> **Argomenti**<br /><br /> Raccolta \(T\), dove T è uno dei tipi seguenti:<br /><br /> Valore `Guid` \(non restituito in SQL Server 2000\),<br /><br /> `Boolean`, `Double`, `DateTime`, `DateTimeOffset`, `Time`, `String` o `Binary`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int32`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_COUNT](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_count)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_COUNT](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_count)]|  
|`COUNT_BIG(` `expression` `)`|Restituisce il numero di elementi in una raccolta come un valore `bigint`.<br /><br /> **Argomenti**<br /><br /> Raccolta \(T\), dove T è uno dei tipi seguenti:<br /><br /> Valore `Guid` \(non restituito in SQL Server 2000\), `Boolean`, `Double`, `DateTime`, `DateTimeOffset`, `Time`, `String` o `Binary`.<br /><br /> **Valore restituito**<br /><br /> Tipo `Int64`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_COUNTBIG](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_countbig)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_COUNTBIG](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_countbig)]|  
|`MAX(` `expression` `)`|Restituisce il valore massimo nella raccolta.<br /><br /> **Argomenti**<br /><br /> Raccolta \(T\), dove T è uno dei tipi seguenti: `Byte`, `Int16`, `Int32`, `Int64`, `Byte`, `Single`, `Double`, `Decimal`, `DateTime`, `DateTimeOffset`, `Time`, `String`, `Binary`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_MAX](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_max)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_MAX](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_max)]|  
|`MIN(` `expression` `)`|Restituisce il valore minimo in una raccolta.<br /><br /> **Argomenti**<br /><br /> Raccolta \(T\), dove T è uno dei tipi seguenti: `Byte`, `Int16`, `Int32`, `Int64`, `Byte`, `Single`, `Double`, `Decimal`, `DateTime`, `DateTimeOffset`, `Time`, `String`,<br /><br /> `Binary`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_MIN](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_min)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_MIN](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_min)]|  
|`STDEV(` `expression` `)`|Restituisce la deviazione statistica standard di tutti i valori nell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> Raccolta \(`Double`\).<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_STDEV](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_stdev)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_STDEV](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdev)]|  
|`STDEVP(` `expression` `)`|Restituisce la deviazione statistica standard relativa alla popolazione per tutti i valori dell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> Raccolta \(`Double`\).<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_STDEVP](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_stdevp)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_STDEVP](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdevp)]|  
|`SUM(` `expression` `)`|Restituisce la somma di tutti i valori della raccolta.<br /><br /> **Argomenti**<br /><br /> Raccolta \(T\), dove T è uno dei tipi seguenti: `Int32`, `Int64`, `Double`, `Decimal`.<br /><br /> **Valore restituito**<br /><br /> Tipo di `expression`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_SUM](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_sum)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_SUM](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_sum)]|  
|`VAR(` `expression` `)`|Restituisce la varianza statistica di tutti i valori nell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> Raccolta \(`Double`\).<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_VAR](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_var)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_VAR](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_var)]|  
|`VARP(` `expression` `)`|Restituisce la varianza statistica della popolazione per tutti i valori nell'espressione specificata.<br /><br /> **Argomenti**<br /><br /> Raccolta \(`Double`\).<br /><br /> **Valore restituito**<br /><br /> Oggetto `Double`.<br /><br /> **Esempio**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_VARP](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_varp)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_VARP](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_varp)]|  
  
 Per altre informazioni sulle funzioni di aggregazione supportate da SqlClient, vedere la documentazione relativa alla versione di SQL Server specificata nel file manifesto del provider SqlClient:  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[Funzioni di aggregazione \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115906)|[Funzioni di aggregazione \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkID=115903)|[Funzioni di aggregazione \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115907)|  
  
## Vedere anche  
 [Linguaggio Entity SQL](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)   
 [Funzioni canoniche di aggregazione](../../../../../docs/framework/data/adonet/ef/language-reference/aggregate-canonical-functions.md)