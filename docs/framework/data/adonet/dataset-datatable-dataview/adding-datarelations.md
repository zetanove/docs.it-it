---
title: "Aggiunta di DataRelation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4a564fb-c1c4-4135-b6c2-b030e51195e4
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Aggiunta di DataRelation
In un <xref:System.Data.DataSet> contenente più oggetti <xref:System.Data.DataTable> è possibile usare gli oggetti <xref:System.Data.DataRelation> per creare relazioni tra le tabelle, navigare tra di esse e restituire le righe padre o figlio da una tabella correlata.  
  
 Gli argomenti necessari per la creazione di un oggetto **DataRelation** sono un nome per l'oggetto **DataRelation** creato e una matrice di uno o più riferimenti <xref:System.Data.DataColumn> alle colonne che fungono da colonne padre e figlio nella relazione.  Una volta creato un oggetto **DataRelation**, è possibile usare tale oggetto per navigare tra le tabelle e recuperare i valori.  
  
 Se si aggiunge un oggetto **DataRelation** a un <xref:System.Data.DataSet>, per impostazione predefinita viene aggiunto un vincolo <xref:System.Data.UniqueConstraint> alla tabella padre e un vincolo <xref:System.Data.ForeignKeyConstraint> alla tabella figlio.  Per altre informazioni su questi vincoli predefiniti, vedere [Vincoli di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md).  
  
 Nell'esempio di codice seguente viene creato un oggetto **DataRelation** usando due oggetti <xref:System.Data.DataTable> in un <xref:System.Data.DataSet>.  In ogni <xref:System.Data.DataTable> è contenuta una colonna denominata **CustID**, che funge da collegamento tra i due oggetti <xref:System.Data.DataTable>.  Nell'esempio viene aggiunto un singolo oggetto **DataRelation** alla raccolta **Relations** del <xref:System.Data.DataSet>.  Il nome dell'oggetto **DataRelation** creato viene specificato dal primo argomento dell'esempio.  Il secondo argomento consente di impostare l'oggetto **DataColumn** padre e il terzo argomento consente di impostare l'oggetto **DataColumn** figlio.  
  
```vb  
customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustID"), _  
  customerOrders.Tables("Orders").Columns("CustID"))  
```  
  
```csharp  
customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustID"],  
  customerOrders.Tables["Orders"].Columns["CustID"]);  
```  
  
 Un oggetto **DataRelation** dispone anche di una proprietà **Nested** che, se impostata su **true**, provoca l'annidamento delle righe della tabella figlio all'interno della riga associata della tabella padre, nel caso in cui tali righe siano scritte come elementi XML tramite il metodo <xref:System.Data.DataSet.WriteXml%2A>.  Per altre informazioni, vedere [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md).  
  
## Vedere anche  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)