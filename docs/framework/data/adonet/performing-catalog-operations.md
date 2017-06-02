---
title: "Esecuzione di operazioni nel catalogo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Esecuzione di operazioni nel catalogo
Per eseguire un comando che modifica un database o un catalogo, ad esempio l'istruzione CREATE TABLE o CREATE PROCEDURE, creare un oggetto **Command** usando le istruzioni SQL appropriate e l'oggetto **Connection**.  Eseguire il comando con il metodo **ExecuteNonQuery** dell'oggetto **Command**.  
  
 Nell'esempio di codice seguente viene creata una stored procedure in un database Microsoft SQL Server.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim queryString As String = "CREATE PROCEDURE InsertCategory " & _  
    "@CategoryName nchar(15), " & _  
    "@Identity int OUT " & _  
    "AS " & _  
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " & _  
    "SET @Identity = @@Identity " & _  
    "RETURN @@ROWCOUNT"  
  
Dim command As SqlCommand = New SqlCommand(queryString, connection)  
command.ExecuteNonQuery()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
string queryString = "CREATE PROCEDURE InsertCategory  " +   
    "@CategoryName nchar(15), " +  
    "@Identity int OUT " +  
    "AS " +   
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " +   
    "SET @Identity = @@Identity " +  
    "RETURN @@ROWCOUNT";  
  
SqlCommand command = new SqlCommand(queryString, connection);  
command.ExecuteNonQuery();  
```  
  
## Vedere anche  
 [Utilizzo di oggetti Command per la modifica dei dati](../../../../docs/framework/data/adonet/using-commands-to-modify-data.md)   
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)