---
title: "Inferenza delle relazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fa86a9d-6545-4a9d-b1f5-58d9742179c7
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Inferenza delle relazioni
Se a un elemento inferito come tabella è associato un elemento figlio a sua volta inferito come tabella, tra le due tabelle verrà creato un tipo <xref:System.Data.DataRelation>.  Una nuova colonna denominata **ParentTableName\_Id** verrà aggiunta alla tabella creata per l'elemento padre e alla tabella creata per l'elemento figlio.  La proprietà **ColumnMapping** della colonna Identity verrà impostata su **MappingType.Hidden**.  La colonna sarà una chiave primaria con incremento automatico per la tabella padre e verrà usata per la **DataRelation** tra le due tabelle.  Il tipo di dati della colonna Identity aggiunta sarà **System.Int32**, a differenza del tipo di dati di tutte le altre colonne inferite, che è **System.String**.  Usando la nuova colonna nelle tabelle padre e figlio, verrà inoltre creato il tipo <xref:System.Data.ForeignKeyConstraint> con la proprietà **DeleteRule** impostata su **Cascade**.  
  
 Ad esempio, si consideri il seguente codice XML:  
  
```  
<DocumentElement>  
  <Element1>  
    <ChildElement1 attr1="value1" attr2="value2"/>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 Dal processo di inferenza verranno prodotte due tabelle: **Element1** e **ChildElement1**.  
  
 Nella tabella **Element1** saranno presenti due colonne: **Element1\_Id** e **ChildElement2**.  La proprietà **ColumnMapping** della colonna **Element1\_Id** verrà impostata su **MappingType.Hidden**.  La proprietà **ColumnMapping** della colonna **ChildElement2** verrà impostata su **MappingType.Element**.  La colonna **Element1\_Id** verrà impostata come chiave primaria della tabella **Element1**.  
  
 Nella tabella **ChildElement1** saranno presenti tre colonne: **attr1**, **attr2** e **Element1\_Id**.  La proprietà **ColumnMapping** per le colonne **attr1** e **attr2** verrà impostata su **MappingType.Attribute**.  La proprietà **ColumnMapping** della colonna **Element1\_Id** verrà impostata su **MappingType.Hidden**.  
  
 Usando le colonne **Element1\_Id** di entrambe le tabelle verranno creati un oggetto **DataRelation** e un vincolo **ForeignKeyConstraint**.  
  
 **DataSet:** DocumentElement  
  
 **Table:** Element1  
  
|Element1\_Id|ChildElement2|  
|------------------|-------------------|  
|0|Text2|  
  
 **Table:** ChildElement1  
  
|attr1|attr2|Element1\_Id|  
|-----------|-----------|------------------|  
|value1|value2|0|  
  
 **DataRelation:** Element1\_ChildElement1  
  
 **ParentTable:** Element1  
  
 **ParentColumn:** Element1\_Id  
  
 **ChildTable:** ChildElement1  
  
 **ChildColumn:** Element1\_Id  
  
 **Nested:** True  
  
 **ForeignKeyConstraint:** Element1\_ChildElement1  
  
 **Column:** Element1\_Id  
  
 **ParentTable:** Element1  
  
 **ChildTable:** ChildElement1  
  
 **DeleteRule:** Cascade  
  
 **AcceptRejectRule:** None  
  
## Vedere anche  
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [DataRelation annidati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)   
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)