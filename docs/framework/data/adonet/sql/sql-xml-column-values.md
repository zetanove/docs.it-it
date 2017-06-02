---
title: "Valori di colonna XML SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Valori di colonna XML SQL
[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] supporta il nuovo tipo di dati `xml`. Gli sviluppatori possono recuperare set di risultati che includono questo tipo usando il comportamento standard della classe <xref:System.Data.SqlClient.SqlCommand>.  È possibile recuperare una colonna `xml` come qualunque altra colonna \(ad esempio, in un tipo <xref:System.Data.SqlClient.SqlDataReader>\) ma se si desidera lavorare con il contenuto della colonna in formato XML, è necessario usare un tipo <xref:System.Xml.XmlReader>.  
  
## Esempio  
 L'applicazione console seguente seleziona due righe, ciascuna contenente una colonna `xml`, dalla tabella **Sales.Store** nel database **AdventureWorks** per un'istanza <xref:System.Data.SqlClient.SqlDataReader>.  Il valore della colonna `xml` per ciascuna riga viene letto usando il metodo <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> del tipo <xref:System.Data.SqlClient.SqlDataReader>.  Il valore viene archiviato in un tipo <xref:System.Xml.XmlReader>.  Notare che è necessario usare il metodo <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> invece del metodo <xref:System.Data.IDataRecord.GetValue%2A>, se si desidera impostare il contenuto su una variabile <xref:System.Data.SqlTypes.SqlXml>. Il metodo <xref:System.Data.IDataRecord.GetValue%2A> restituisce il valore della colonna `xml` sotto forma di stringa.  
  
> [!NOTE]
>  Per impostazione predefinita, il database di esempio **AdventureWorks** non viene installato insieme a [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Per installarlo, è sufficiente eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
 [!code-csharp[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/VB/source.vb#1)]  
  
## Vedere anche  
 <xref:System.Data.SqlTypes.SqlXml>   
 [Dati XML in SQL Server](../../../../../docs/framework/data/adonet/sql/xml-data-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)