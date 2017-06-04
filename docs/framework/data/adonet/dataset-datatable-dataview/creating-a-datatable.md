---
title: "Creazione di una DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eecf9d78-60e3-4fdc-8de0-e56c13a89414
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Creazione di una DataTable
È possibile creare una <xref:System.Data.DataTable>, che rappresenta una tabella di dati relazionali in memoria, e usarla in modo indipendente oppure usarla tramite altri oggetti di .NET Framework, in genere come membro di un <xref:System.Data.DataSet>.  
  
 È possibile creare un oggetto **DataTable** usando il costruttore **DataTable** appropriato.  È possibile aggiungerlo al **DataSet** usando il metodo **Add** per aggiungerlo alla raccolta **Tables** dell'oggetto **DataTable**.  
  
 È inoltre possibile creare oggetti **DataTable** all'interno di un **DataSet** tramite i metodi **Fill** o **FillSchema** dell'oggetto **DataAdapter** oppure partendo da uno schema XML predefinito o inferito usando i metodi **ReadXml**, **ReadXmlSchema** o **InferXmlSchema** del **DataSet**.  Notare che dopo l'aggiunta di una **DataTable** come membro di una raccolta **Tables** di un **DataSet**, non sarà possibile aggiungerla a raccolte di tabelle di altri **DataSet**.  
  
 Una **DataTable** appena creata non dispone di alcuno schema, ovvero di una struttura.  Per definire lo schema della tabella, è necessario creare e aggiungere oggetti <xref:System.Data.DataColumn> alla raccolta **Columns** della tabella.  È inoltre possibile definire una colonna di chiavi primarie per la tabella e creare e aggiungere oggetti **Constraint** alla raccolta **Constraints** della tabella.  Una volta definito lo schema per una **DataTable**, è possibile aggiungere righe di dati alla tabella tramite l'aggiunta di oggetti **DataRow** alla raccolta **Rows** della tabella.  
  
 Quando si crea una **DataTable**, non è necessario fornire un valore per la proprietà <xref:System.Data.DataTable.TableName%2A>. È possibile specificare in seguito tale proprietà o lasciarla vuota.  Tuttavia, se si aggiunge una tabella priva del valore **TableName** al **DataSet**, a tale tabella verrà assegnato il nome incrementale predefinito Table*N*, a partire da "Table" per Table0.  
  
> [!NOTE]
>  Si consiglia di evitare la convenzione di denominazione "Column*N*" quando si fornisce un valore per **TableName**, poiché è possibile che il nome fornito sia in conflitto con un nome di colonna predefinito esistente nel **DataSet**.  Se il nome fornito è già presente, viene generata un'eccezione.  
  
 Nell'esempio seguente viene creata un'istanza di un oggetto **DataTable** e viene assegnato a tale oggetto il nome "Customers".  
  
```vb  
Dim workTable as DataTable = New DataTable("Customers")  
  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
```  
  
 Nell'esempio seguente viene creata un'istanza di un oggetto **DataTable** aggiungendo l'oggetto alla raccolta **Tables** di un **DataSet**.  
  
```vb  
Dim customers As DataSet = New DataSet  
Dim customersTable As DataTable = _  
   customers.Tables.Add("CustomersTable")  
  
```  
  
```csharp  
DataSet customers = new DataSet();  
DataTable customersTable = customers.Tables.Add("CustomersTable");  
```  
  
## Vedere anche  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataTableCollection>   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Popolamento di un dataset da un oggetto DataAdapter](../../../../../docs/framework/data/adonet/populating-a-dataset-from-a-dataadapter.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)