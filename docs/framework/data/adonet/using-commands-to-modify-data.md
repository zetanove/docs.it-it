---
title: "Utilizzo di oggetti Command per la modifica dei dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Utilizzo di oggetti Command per la modifica dei dati
Con un provider di dati .NET Framework è possibile eseguire stored procedure o istruzioni DDL \(Data Definition Language\), ad esempio CREATE TABLE e ALTER COLUMN, per modificare lo schema di un database o di un catalogo.  Poiché, diversamente dalle query, questi comandi non restituiscono righe, l'oggetto **Command** fornisce un metodo **ExecuteNonQuery** per l'elaborazione.  
  
 Oltre a usare **ExecuteNonQuery** per modificare lo schema, è possibile usare questo metodo per elaborare istruzioni SQL che modificano i dati ma non restituiscono righe, ad esempio INSERT, UPDATE e DELETE.  
  
 Anche se il metodo **ExecuteNonQuery** non restituisce righe, è possibile passare e restituire parametri di input e di output e valori restituiti mediante la raccolta **Parameters** dell'oggetto **Command**.  
  
## In questa sezione  
 [Aggiornamento dei dati in un'origine dati](../../../../docs/framework/data/adonet/updating-data-in-a-data-source.md)  
 Viene descritto come eseguire i comandi o le stored procedure che modificano i dati in un database.  
  
 [Esecuzione di operazioni nel catalogo](../../../../docs/framework/data/adonet/performing-catalog-operations.md)  
 Viene descritto come eseguire i comandi per la modifica dello schema di database.  
  
## Vedere anche  
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)