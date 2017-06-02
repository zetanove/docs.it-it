---
title: "Aggiunta di una DataTable a un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 556d29a3-8fc9-4e38-b3ee-c188f7e7b155
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Aggiunta di una DataTable a un DataSet
ADO.NET consente di creare oggetti <xref:System.Data.DataTable> e di aggiungerli a un tipo <xref:System.Data.DataSet> esistente.  È possibile impostare le informazioni relative ai vincoli per un tipo <xref:System.Data.DataTable> usando le proprietà <xref:System.Data.DataTable.PrimaryKey%2A> e <xref:System.Data.DataColumn.Unique%2A>.  
  
## Esempio  
 L'esempio seguente consente di creare un tipo <xref:System.Data.DataSet>, aggiungere un nuovo oggetto <xref:System.Data.DataTable> al <xref:System.Data.DataSet> e aggiungere tre oggetti <xref:System.Data.DataColumn> alla tabella.  Il codice consente infine di impostare una colonna come colonna di chiave primaria.  
  
 [!code-csharp[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/VB/source.vb#1)]  
  
## Distinzione fra maiuscole e minuscole  
 In un tipo <xref:System.Data.DataSet> sono consentite due o più tabelle o relazioni con lo stesso nome ma con diversa combinazione di maiuscole e minuscole.  In questi casi, i riferimenti basati sui nomi a tabelle e relazioni prevedono la distinzione tra maiuscole e minuscole.  Se ad esempio in un tipo <xref:System.Data.DataSet> **dataSet** sono contenute le tabelle **Table1** e **table1**, il riferimento basato sul nome a **Table1** sarà **dataSet.Tables\["Table1"\]** e il riferimento a **table1** sarà **dataSet.Tables\["table1"\]**.  Se si tenta di fare riferimento a una delle due tabelle come **dataSet.Tables\["TABLE1"\]**, verrà generata un'eccezione.  
  
 La distinzione tra maiuscole e minuscole non è rilevante se è presente solo una tabella o relazione con un determinato nome.  Se ad esempio nel tipo <xref:System.Data.DataSet> è presente solo **Table1**, è possibile fare riferimento a questa tabella usando **dataSet.Tables\["TABLE1"\]**.  
  
> [!NOTE]
>  La proprietà <xref:System.Data.DataSet.CaseSensitive%2A> del tipo <xref:System.Data.DataSet> non influisce su tale comportamento.  La proprietà <xref:System.Data.DataSet.CaseSensitive%2A> viene infatti applicata ai dati del tipo <xref:System.Data.DataSet> e influisce sull'ordinamento, la ricerca, l'applicazione di filtri, di vincoli e così via.  
  
## Supporto dello spazio dei nomi  
 Nelle versioni ADO.NET precedenti alla 2.0 due tabelle non potevano avere lo stesso nome, anche se si trovavano in spazi dei nomi diversi.  In ADO.NET 2.0 questa limitazione è stata eliminata.  Un tipo <xref:System.Data.DataSet> può contenere due tabelle con lo stesso valore per la proprietà <xref:System.Data.DataTable.TableName%2A> ma con valori diversi per la proprietà <xref:System.Data.DataTable.Namespace%2A>.  
  
## Vedere anche  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)