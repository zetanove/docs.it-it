---
title: "Inferenza di colonne | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e022699-c922-454c-93e2-957dd7e7247a
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Inferenza di colonne
Una volta che ADO.NET ha determinato quali elementi di un documento XML devono essere inferiti come tabelle per un tipo <xref:System.Data.DataSet>, vengono inferite le colonne di tali tabelle.  In ADO.NET 2.0 è stato introdotto un nuovo motore di inferenza dello schema che consente di inferire un tipo di dati tipizzato per ogni elemento **simpleType**.  Nelle versioni precedenti il tipo di dati di un elemento **simpleType** inferito era sempre **xsd:string**.  
  
## Migrazione e compatibilità con versioni precedenti  
 Il metodo **ReadXml** accetta un argomento di tipo **InferSchema**.  Tale argomento consente di specificare il comportamento di inferenza compatibile con versioni precedenti.  Nella tabella seguente sono indicati i valori disponibili per l'enumerazione **InferSchema**:  
  
 <xref:System.Data.XmlReadMode>  
 Fornisce compatibilità con le versioni precedenti inferendo sempre un tipo semplice come <xref:System.String>.  
  
 <xref:System.Data.XmlReadMode>  
 Inferisce un tipo di dati tipizzato in modo sicuro.  Viene generata un'eccezione se usato con un tipo <xref:System.Data.DataTable>.  
  
 <xref:System.Data.XmlReadMode>  
 Ignora tutti gli schemi inline e legge i dati nello schema <xref:System.Data.DataSet> esistente.  
  
## Attributi  
 Come definito nella sezione [Inferenza di tabelle](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-tables.md), un elemento con attributi verrà inferito come tabella.  Gli attributi di tale elemento verranno quindi inferiti come colonne della tabella.  La proprietà **ColumnMapping** delle colonne verrà impostata su **MappingType.Attribute**, per assicurare che i nomi delle colonne vengano scritti come attributi in caso di riconversione in XML dello schema.  I valori degli attributi vengono archiviati in una riga della tabella.  Ad esempio, si consideri il seguente codice XML:  
  
```  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 Il processo di inferenza genererà una tabella denominata **Element1** con due colonne, ovvero **attr1** e **attr2**.  La proprietà **ColumnMapping** per entrambe le colonne verrà impostata su **MappingType.Attribute**.  
  
 **DataSet:** DocumentElement  
  
 **Table:** Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## Elementi privi di attributi o elementi figlio  
 Se un elemento non dispone di elementi figlio o attributi, tale elemento verrà inferito come colonna.  La proprietà **ColumnMapping** della colonna verrà impostata su **MappingType.Element**.  Il testo degli elementi figlio è archiviato in una riga della tabella.  Ad esempio, si consideri il seguente codice XML:  
  
```  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 Il processo di inferenza genererà una tabella denominata **Element1** con due colonne, ovvero **ChildElement1** e **ChildElement2**.  La proprietà **ColumnMapping** per entrambe le colonne verrà impostata su **MappingType.Element**.  
  
 **DataSet:** DocumentElement  
  
 **Table:** Element1  
  
|ChildElement1|ChildElement2|  
|-------------------|-------------------|  
|Text1|Text2|  
  
## Vedere anche  
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)