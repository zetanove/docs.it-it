---
title: "Inferenza del testo degli elementi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 789799e5-716f-459f-a168-76c5cf22178b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Inferenza del testo degli elementi
Se in un elemento è presente del testo ma a tale elemento non sono associati elementi figlio da inferire come tabelle \(quali elementi con attributi o elementi ripetuti\), una nuova colonna denominata **TableName\_Text** verrà aggiunta alla tabella inferita per l'elemento.  Il testo contenuto nell'elemento viene aggiunto a una riga della tabella e archiviato nella nuova colonna.  La proprietà **ColumnMapping** della nuova colonna viene impostata su **MappingType.SimpleContent**.  
  
 Ad esempio, si consideri il seguente codice XML.  
  
```  
<DocumentElement>  
  <Element1 attr1="value1">Text1</Element1>  
</DocumentElement>  
```  
  
 Il processo di inferenza genererà una tabella denominata **Element1** con due colonne, ovvero **attr1** e **Element1\_Text**.  La proprietà **ColumnMapping** della colonna **attr1** verrà impostata su **MappingType.Attribute**.  La proprietà **ColumnMapping** della colonna  **Element1\_Text** verrà impostata su **MappingType.SimpleContent**.  
  
 **DataSet:** DocumentElement  
  
 **Table:** Element1  
  
|attr1|Element1\_Text|  
|-----------|--------------------|  
|value1|Text1|  
  
 Se in un elemento è presente del testo ma a tale elemento sono associati anche elementi figlio contenenti testo, alla tabella non verrà aggiunta alcuna colonna in cui archiviare il testo contenuto nell'elemento.  Il testo contenuto nell'elemento verrà ignorato e il testo degli elementi figlio viene incluso in una riga della tabella.  Ad esempio, si consideri il seguente codice XML.  
  
```  
<Element1>  
  Text1  
  <ChildElement1>Text2</ChildElement1>  
  Text3  
</Element1>  
```  
  
 Il processo di inferenza produrrà una tabella denominata **Element1** con una sola colonna denominata **ChildElement1**.  Il testo dell'elemento **ChildElement1** verrà incluso in una riga della tabella.  Il testo rimanente verrà ignorato.  La proprietà **ColumnMapping** della colonna **ChildElement1** verrà impostata su **MappingType.Element**.  
  
 **DataSet:** DocumentElement  
  
 **Table:** Element1  
  
|ChildElement1|  
|-------------------|  
|Text2|  
  
## Vedere anche  
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)