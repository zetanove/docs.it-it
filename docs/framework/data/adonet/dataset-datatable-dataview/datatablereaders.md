---
title: "DataTableReader | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97546ae2-0e42-4d26-961d-e0b244d81ded
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataTableReader
Il tipo <xref:System.Data.DataTableReader> presenta il contenuto di un tipo <xref:System.Data.DataTable> o di un tipo <xref:System.Data.DataSet> sotto forma di uno o più set di risultati forward\-only in sola lettura.  
  
 Quando si crea un **DataTableReader** da una **DataTable**, l'oggetto **DataTableReader** risultante contiene un solo set di risultati con gli stessi dati della **DataTable** da cui è stato creato, ad eccezione delle righe contrassegnate come eliminate.  Le colonne vengono visualizzate nello stesso ordine in cui vengono visualizzate nella **DataTable** originale.  
  
 Un **DataTableReader** può contenere più set di risultati se viene creato chiamando il metodo <xref:System.Data.DataSet.CreateDataReader%2A>.  L'ordine dei risultati corrisponde a quello delle **DataTable** nella raccolta <xref:System.Data.DataSet.Tables%2A> dell'oggetto **DataSet**.  
  
## In questa sezione  
 [Creazione di un DataReader](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-datareader.md)  
 Viene illustrato come creare un oggetto **DataTableReader**.  
  
 [Navigazione in DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/navigating-datatables.md)  
 Viene descritto come usare il metodo **Read** per spostarsi all'interno del contenuto di un **DataTableReader**.  
  
## Vedere anche  
 [Recupero e modifica di dati in ADO.NET](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)