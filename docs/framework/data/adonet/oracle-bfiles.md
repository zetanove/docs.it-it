---
title: "BFILE Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 341bbf84-4734-4d44-8723-ccedee954e21
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# BFILE Oracle
Il provider di dati .NET Framework per Oracle include la classe <xref:System.Data.OracleClient.OracleBFile>, usata per i tipi di dati <xref:System.Data.OracleClient.OracleType> Oracle.  
  
 Il tipo di dati **BFILE** Oracle è un tipo di dati **LOB** Oracle in cui è presente un riferimento a dati binari con una dimensione massima di 4 GB.  Un **BFILE** Oracle si differenzia da altri tipi di dati **LOB** Oracle in quanto i dati del primo sono archiviati in un file fisico nel sistema operativo, anziché sul server.  Il tipo di dati **BFILE** fornisce l'accesso in sola lettura ai dati.  
  
 Di seguito vengono elencate altre caratteristiche che distinguono un tipo di dati **BFILE** da un tipo di dati **LOB**:  
  
-   Contiene dati non strutturati.  
  
-   Supporta il chunking sul lato server.  
  
-   Usa la semantica di copia di riferimenti.  Se ad esempio si esegue un'operazione di copia su un **BFILE**, viene copiato solo l'indicatore di posizione del **BFILE** che rappresenta un riferimento al file.  I dati nel file non vengono copiati.  
  
 È necessario usare il tipo di dati **BFILE** per fare riferimento a LOB di grandi dimensioni e quindi poco pratici da archiviare nel database.  L'utilizzo di un tipo di dati **BFILE** provoca un sovraccarico su client, server e comunicazioni rispetto al tipo di dati **LOB**.  È preferibile accedere a un **BFILE** se è necessario ottenere solo una quantità di dati limitata.  Se è necessario ottenere l'intero oggetto, è opportuno accedere a LOB residenti nel database.  
  
 Ciascun oggetto **OracleBFile** non NULL è associato a due entità che definiscono la posizione del file fisico sottostante:  
  
1.  Un oggetto DIRECTORY Oracle, che è un alias del database per una directory nel file system e  
  
2.  Il nome del file fisico sottostante, che si trova nella directory associata all'oggetto DIRECTORY.  
  
## Esempio  
 Nell'esempio in C\# seguente viene illustrato come creare un **BFILE** in una tabella Oracle, quindi come recuperarlo sotto forma di oggetto **OracleBFile**.  L'esempio mostra come usare l'oggetto <xref:System.Data.OracleClient.OracleDataReader> e i metodi **OracleBFile** **Seek** e **Read**.  Notare che per usare questo esempio, è innanzitutto necessario creare sul server Oracle una directory denominata "c:\\\\bfiles" e un file denominato "MyFile.jpg".  
  
```csharp  
using System;  
using System.IO;  
using System.Data;  
using System.Data.OracleClient;  
  
public class Sample  
{  
   public static void Main(string[] args)  
   {  
      OracleConnection connection = new OracleConnection(  
        "Data Source=Oracle8i;Integrated Security=yes");  
      connection.Open();  
  
      OracleCommand command = connection.CreateCommand();  
      command.CommandText =   
        "CREATE or REPLACE DIRECTORY MyDir as 'c:\\bfiles'";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "DROP TABLE MyBFileTable";  
      try {  
        command.ExecuteNonQuery();  
      }  
      catch {  
      }  
      command.CommandText =   
        "CREATE TABLE MyBFileTable(col1 number, col2 BFILE)";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "INSERT INTO MyBFileTable values ('2', BFILENAME('MyDir', " +  
        "'MyFile.jpg'))";  
      command.ExecuteNonQuery();  
      command.CommandText = "SELECT * FROM MyBFileTable";  
  
        byte[] buffer = new byte[100];  
  
      OracleDataReader reader = command.ExecuteReader();  
      using (reader) {  
          if (reader.Read()) {  
                OracleBFile bFile = reader.GetOracleBFile(1);  
                using (bFile) {  
                  bFile.Seek(0, SeekOrigin.Begin);  
                  bFile.Read(buffer, 0, 100);  
              }  
          }  
      }  
  
      connection.Close();  
   }  
  
}  
```  
  
## Vedere anche  
 [Oracle e ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)