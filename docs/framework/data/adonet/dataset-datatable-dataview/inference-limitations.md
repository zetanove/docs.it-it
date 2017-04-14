---
title: "Limitazioni delle inferenze | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 78517994-5d57-44f8-9d20-38812977de09
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Limitazioni delle inferenze
Il processo di inferenza di uno schema di un tipo <xref:System.Data.DataSet> da un documento XML può fornire come risultato diversi schemi a seconda degli elementi XML presenti in ogni documento.  Si considerino ad esempio i seguenti documenti XML:  
  
 Document1:  
  
```  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 Document2:  
  
```  
<DocumentElement>  
  <Element1>Text1</Element1>  
</DocumentElement>  
```  
  
 Nel caso di "Document1", il processo di inferenza consente di produrre un **DataSet** denominato "DocumentElement" e una tabella denominata "Element1", poiché "Element1" è un elemento ripetuto.  
  
 **DataSet:** DocumentElement  
  
 **Table:** Element1  
  
|Element1\_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
 Tuttavia, nel caso di "Document2", il processo di inferenza consente di produrre un oggetto **DataSet** denominato "NewDataSet" e una tabella denominata "DocumentElement". "Element1" viene inferito come colonna in quanto privo di attributi o elementi figlio.  
  
 **DataSet:** NewDataSet  
  
 **Table:** DocumentElement  
  
|Element1|  
|--------------|  
|Text1|  
  
 È possibile che lo scopo di tali documenti XML fosse la creazione dello stesso schema, ma il processo di inferenza consente di produrre risultati molto diversi in base agli elementi contenuti in ogni documento.  
  
 Per evitare eventuali discrepanze nella generazione di uno schema da un documento XML, si consiglia di specificare esplicitamente uno schema tramite il linguaggio XSD \(XML Schema Definition Language\) o XDR \(XML\-Data Reduced\) durante il caricamento di un **DataSet** da XML.  Per altre informazioni su come specificare in modo esplicito lo schema di un **DataSet** con XML Schema, vedere [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md).  
  
## Vedere anche  
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)