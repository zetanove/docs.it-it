---
title: "Aggiunta di vincoli esistenti a un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Aggiunta di vincoli esistenti a un DataSet
Il metodo **Fill** di **DataAdapter** consente di compilare un <xref:System.Data.DataSet> solo con colonne e righe di tabella di un'origine dati. Sebbene i vincoli vengano in genere impostati dall'origine dati, per impostazione predefinita il metodo **Fill** non aggiunge queste informazioni sullo schema al **DataSet**.  Per compilare un **DataSet** con le informazioni esistenti sui vincoli della chiave primaria da un'origine dati, è possibile chiamare il metodo **FillSchema** di **DataAdapter** oppure impostare la proprietà **MissingSchemaAction** di **DataAdapter** su **AddWithKey** prima di chiamare **Fill**.  Ciò garantisce che i vincoli della chiave primaria nel **DataSet** riflettano quelli nell'origine dati.  Le informazioni sul vincolo di chiave esterna non sono incluse e devono essere create in modo esplicito, come illustrato in [Vincoli di DataTable](../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md).  
  
 L'aggiunta delle informazioni sullo schema in un **DataSet** prima di compilarlo con i dati assicura che i vincoli della chiave primaria siano inclusi negli oggetti <xref:System.Data.DataTable> e **DataSet**.  In questo modo, quando vengono effettuate altre chiamate per compilare il **DataSet**, le informazioni nella colonna della chiave primaria vengono usate per confrontare le nuove righe provenienti dall'origine dati con le righe correnti in ogni **DataTable** e i dati correnti nelle tabelle vengono sovrascritti con i dati provenienti dall'origine dati.  Senza le informazioni sullo schema, le nuove righe provenienti dall'origine dati verrebbero aggiunte al **DataSet** generando righe duplicate.  
  
> [!NOTE]
>  Se una colonna in un'origine dati viene identificata come colonna con incremento automatico, il metodo **FillSchema**, o il metodo **Fill** con la proprietà **MissingSchemaAction** impostata su **AddWithKey**, crea un oggetto **DataColumn** con una proprietà **AutoIncrement** impostata su `true`.  È tuttavia necessario impostare direttamente i valori di **AutoIncrementStep** e **AutoIncrementSeed**.  Per altre informazioni sulle colonne con incremento automatico, vedere [Creazione di colonne AutoIncrement](../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-autoincrement-columns.md).  
  
 Se si usa **FillSchema** o si imposta **MissingSchemaAction** su **AddWithKey**, è necessaria un'elaborazione aggiuntiva nell'origine dati per determinare le informazioni della colonna della chiave primaria.  Questa ulteriore elaborazione può ridurre le prestazioni.  Se le informazioni sulla chiave primaria sono note in fase di progettazione, è consigliabile specificare la colonna o le colonne della chiave primaria in modo esplicito per migliorare le prestazioni.  Per altre informazioni sull'impostazione esplicita delle informazioni sulla chiave primaria per una tabella, vedere [Definizione di chiavi primarie](../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md).  
  
 Nell'esempio di codice seguente viene descritto come aggiungere le informazioni sullo schema a un **DataSet** usando **FillSchema**.  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers")  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers");  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
 Nell'esempio di codice seguente viene descritto come aggiungere le informazioni sullo schema a un **DataSet** usando la proprietà **MissingSchemaAction.AddWithKey** del metodo **Fill**.  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
## Gestione di più set di risultati  
 Se l'oggetto **DataAdapter** rileva più set di risultati restituiti da **SelectCommand**, verranno create più tabelle nel **DataSet**.  Alle tabelle viene assegnato un nome predefinito incrementale in base zero **Table** *N*, che inizia con **Table** anziché con "Table0".  Se il nome di una tabella viene passato come argomento al metodo **FillSchema**, alle tabelle verrà assegnato il nome incrementale in base zero **TableName** *N*, che inizia con **TableName** anziché con "TableName0".  
  
> [!NOTE]
>  Se il metodo **FillSchema** dell'oggetto **OleDbDataAdapter** viene chiamato per un comando che restituisce più set di risultati, vengono restituite solo le informazioni sullo schema del primo set di risultati.  Quando vengono restituite informazioni sullo schema per più set di risultati usando **OleDbDataAdapter**, è consigliabile impostare **MissingSchemaAction** su **AddWithKey** e ottenere le informazioni sullo schema quando si chiama il metodo **Fill**.  
  
## Vedere anche  
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [DataSet, DataTable e DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)