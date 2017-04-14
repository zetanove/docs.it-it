---
title: "Aggiunta di colonne a un DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e85c4a0e-4f3f-458c-b58b-0ddbc06bf974
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Aggiunta di colonne a un DataTable
In una <xref:System.Data.DataTable> è contenuta una raccolta di oggetti <xref:System.Data.DataColumn> a cui fa riferimento la proprietà **Columns** della tabella.  Tale raccolta di colonne, insieme a eventuali vincoli, consente di definire lo schema, o struttura, della tabella.  
  
 È possibile creare oggetti **DataColumn** all'interno di una tabella tramite il costruttore **DataColumn** o chiamando il metodo **Add** della proprietà **Columns** della tabella, che è un <xref:System.Data.DataColumnCollection>.  Il metodo **Add** accetta gli argomenti facoltativi **ColumnName**, **DataType** ed **Expression** e crea un nuovo **DataColumn** come membro della raccolta.  Tale metodo accetta inoltre un oggetto **DataColumn** e lo aggiunge alla raccolta. Se richiesto, restituisce un riferimento al **DataColumn** aggiunto.  Poiché gli oggetti **DataTable** non sono specifici di alcuna origine dati, i tipi di .NET Framework vengono usati quando si specifica il tipo di dati di un **DataColumn**.  
  
 Nell'esempio seguente vengono aggiunte quattro colonne a una **DataTable**.  
  
```vb  
Dim workTable As DataTable = New DataTable("Customers")  
  
Dim workCol As DataColumn = workTable.Columns.Add( _  
    "CustID", Type.GetType("System.Int32"))  
workCol.AllowDBNull = false  
workCol.Unique = true  
  
workTable.Columns.Add("CustLName", Type.GetType("System.String"))  
workTable.Columns.Add("CustFName", Type.GetType("System.String"))  
workTable.Columns.Add("Purchases", Type.GetType("System.Double"))  
  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
  
DataColumn workCol = workTable.Columns.Add("CustID", typeof(Int32));  
workCol.AllowDBNull = false;  
workCol.Unique = true;  
  
workTable.Columns.Add("CustLName", typeof(String));  
workTable.Columns.Add("CustFName", typeof(String));  
workTable.Columns.Add("Purchases", typeof(Double));  
```  
  
 Notare che nell'esempio le proprietà per la colonna **CustID** sono impostate in modo da non consentire valori **DBNull** e da applicare vincoli ai valori per assicurarne l'univocità.  Tuttavia, se si definisce la colonna **CustID** come colonna di chiave primaria della tabella, la proprietà **AllowDBNull** verrà impostata automaticamente su **false** e la proprietà **Unique** verrà impostata automaticamente su **true**.  Per altre informazioni, vedere [Definizione di chiavi primarie](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md).  
  
> [!CAUTION]
>  Se a una colonna non viene assegnato alcun nome, questa assumerà il nome predefinito incrementale Column*N*, a partire da "Column1", quando viene aggiunta a **DataColumnCollection**.  Si consiglia di evitare la convenzione di denominazione "Column*N*" quando si fornisce un nome di colonna, poiché è possibile che il nome fornito sia in conflitto con un nome di colonna predefinito esistente nel **DataColumnCollection**.  Se il nome fornito è già presente, viene generata un'eccezione.  
  
 Se si sta usando l'oggetto <xref:System.Xml.XLinq.XElement> come proprietà <xref:System.Data.DataColumn.DataType%2A> di un oggetto <xref:System.Data.DataColumn> nell'oggetto <xref:System.Data.DataTable>, la serializzazione XML non funzionerà quando si legge nei dati.  Ad esempio, se si scrive un oggetto <xref:System.Xml.XmlDocument> usando il metodo `DataTable.WriteXml`, durante la serializzazione in XML è presente un nodo padre aggiuntivo nell'oggetto <xref:System.Xml.XLinq.XElement>.  Per risolvere questo problema, usare il tipo <xref:System.Data.SqlTypes.SqlXml> invece dell'oggetto <xref:System.Xml.XLinq.XElement>.  `ReadXml` e `WriteXml` funzionano correttamente con l'oggetto <xref:System.Data.SqlTypes.SqlXml>.  
  
## Vedere anche  
 <xref:System.Data.DataColumn>   
 <xref:System.Data.DataColumnCollection>   
 <xref:System.Data.DataTable>   
 [Definizione dello schema di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)