---
title: "Mapping di DataAdapter DataTable e DataColumn | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Mapping di DataAdapter DataTable e DataColumn
Un oggetto **DataAdapter** contiene una raccolta di zero o più oggetti <xref:System.Data.Common.DataTableMapping> nella proprietà **TableMappings**.  Un **DataTableMapping** fornisce un mapping master tra i dati restituiti da una query eseguita su un'origine dati e una <xref:System.Data.DataTable>.  Al posto del nome della **DataTable** è possibile passare il nome di **DataTableMapping** al metodo **Fill** di **DataAdapter**.  Nell'esempio seguente viene creato un **DataTableMapping** denominato **AuthorsMapping** per la tabella **MyAuthors**.  
  
```vb  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors")  
```  
  
```csharp  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");  
```  
  
 Un **DataTableMapping** consente di usare in un **DataTable** nomi di colonne diversi da quelli presenti nel database.  L'oggetto **DataAdapter** usa il mapping per mantenere la corrispondenza delle colonne quando la tabella viene aggiornata.  
  
 Se non si specifica un nome **TableName** o **DataTableMapping** quando si chiama il metodo **Fill** o **Update** di **DataAdapter**, **DataAdapter** cercherà un **DataTableMapping** denominato "Table".  Se tale **DataTableMapping** non esiste, il **TableName** di **DataTable** sarà "Table".  È possibile specificare un **DataTableMapping** predefinito creando un **DataTableMapping** con il nome "Table".  
  
 Nell'esempio di codice seguente viene creato un **DataTableMapping** \(dallo spazio dei nomi <xref:System.Data.Common>\) che viene impostato come mapping predefinito per il **DataAdapter** specificato denominandolo "Table".  Viene quindi eseguito il mapping delle colonne della prima tabella nel set di risultati della query, ovvero la tabella **Customers** del database **Northwind**, a un set di nomi più semplici nella tabella **Northwind Customers** dell'oggetto <xref:System.Data.DataSet>.  Per le colonne di cui non viene eseguito il mapping, viene usato il nome della colonna nell'origine dati.  
  
```vb  
Dim mapping As DataTableMapping = _  
  adapter.TableMappings.Add("Table", "NorthwindCustomers")  
mapping.ColumnMappings.Add("CompanyName", "Company")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode")  
  
adapter.Fill(custDS)  
  
```  
  
```csharp  
DataTableMapping mapping =   
  adapter.TableMappings.Add("Table", "NorthwindCustomers");  
mapping.ColumnMappings.Add("CompanyName", "Company");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode");  
  
adapter.Fill(custDS);  
```  
  
 In un contesto più avanzato, può essere necessario che lo stesso oggetto **DataAdapter** supporti il caricamento di diverse tabelle con mapping diversi.  A tale scopo è sufficiente aggiungere altri oggetti **DataTableMapping**.  
  
 Quando al metodo **Fill** vengono passati un'istanza di un **DataSet** e un nome di **DataTableMapping**, viene usato un mapping con quel nome, se esistente, in caso contrario viene usato un **DataTable** con quel nome.  
  
 Nell'esempio seguente viene creato un **DataTableMapping** con il nome **Customers** e viene assegnato il nome **BizTalkSchema** a una **DataTable**.  Viene quindi eseguito il mapping delle righe restituite dall'istruzione SELECT alla **DataTable** **BizTalkSchema**.  
  
```vb  
Dim mapping As ITableMapping = _  
  adapter.TableMappings.Add("Customers", "BizTalkSchema")  
mapping.ColumnMappings.Add("CustomerID", "ClientID")  
mapping.ColumnMappings.Add("CompanyName", "ClientName")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIP")  
  
adapter.Fill(custDS, "Customers")  
  
```  
  
```csharp  
ITableMapping mapping =   
  adapter.TableMappings.Add("Customers", "BizTalkSchema");  
mapping.ColumnMappings.Add("CustomerID", "ClientID");  
mapping.ColumnMappings.Add("CompanyName", "ClientName");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIP");  
  
adapter.Fill(custDS, "Customers");  
```  
  
> [!NOTE]
>  Se non viene indicato il nome della colonna di origine per il mapping di una colonna o il nome della tabella di origine per il mapping di una tabella, vengono generati automaticamente nomi predefiniti.  Se non viene indicato il nome della colonna di origine, al mapping della colonna viene assegnato il nome predefinito incrementale **SourceColumn** *N*, che inizia con **SourceColumn1**.  Se non viene indicato il nome della tabella di origine, al mapping della tabella viene assegnato il nome predefinito incrementale **SourceTable** *N*, che inizia con **SourceTable1**.  
  
> [!NOTE]
>  Si consiglia di evitare la convenzione di denominazione di **SourceColumn** *N* per il mapping di una colonna o di **SourceTable** *N* per il mapping di una tabella, in quanto il nome indicato può entrare in conflitto con il nome predefinito esistente del mapping di una colonna in **ColumnMappingCollection** o con il nome del mapping di una tabella in **DataTableMappingCollection**.  Se il nome specificato esiste già, verrà generata un'eccezione.  
  
## Gestione di più set di risultati  
 Se **SelectCommand** restituisce più tabelle, **Fill** genera automaticamente nomi di tabella con valori incrementali per le tabelle contenute nel **DataSet**, che iniziano con il nome specificato e proseguono nel formato **TableName** *N*, che inizia con **TableName1**.  È possibile eseguire il mapping del nome della tabella generato automaticamente sul nome che si desidera specificare per la tabella nel **DataSet**.  Per un **SelectCommand** che restituisce le due tabelle **Customers** e **Orders**, ad esempio, si esegue la chiamata seguente a **Fill**.  
  
```  
adapter.Fill(customersDataSet, "Customers")  
```  
  
 Vengono create due tabelle nell'oggetto **DataSet**: **Customers** e **Customers1**.  È possibile usare i mapping di tabelle per fare in modo che il nome della seconda tabella sia **Orders** anziché **Customers1**.  A tale scopo, eseguire il mapping della tabella di origine di **Customers1** sulla tabella **Orders** del **DataSet**, come illustrato nell'esempio seguente.  
  
```  
adapter.TableMappings.Add("Customers1", "Orders")  
adapter.Fill(customersDataSet, "Customers")  
```  
  
## Vedere anche  
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)