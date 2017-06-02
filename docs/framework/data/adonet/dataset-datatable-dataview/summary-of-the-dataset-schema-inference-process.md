---
title: "Riepilogo del processo di inferenza dello schema di un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Riepilogo del processo di inferenza dello schema di un DataSet
Il processo di inferenza determina innanzitutto, sulla base del documento XML, quali elementi verranno inferiti come tabelle.  Sulla base delle rimanenti informazioni XML, il processo di inferenza consente quindi di determinare le colonne per tali tabelle.  Nel caso di tabelle annidate, gli oggetti <xref:System.Data.DataRelation> e <xref:System.Data.ForeignKeyConstraint> vengono generati dal processo di inferenza.  
  
 Di seguito viene riportato un breve riepilogo delle regole di inferenza:  
  
-   Gli elementi a cui sono associati attributi vengono inferiti come tabelle.  
  
-   Gli elementi a cui sono associati elementi figlio vengono inferiti come tabelle.  
  
-   Gli elementi ripetuti vengono inferiti come tabella singola.  
  
-   Se all'elemento del documento, o radice, non sono associati attributi ed elementi figlio da inferire come colonne, tale elemento viene inferito come un tipo <xref:System.Data.DataSet>.  In caso contrario, l'elemento del documento viene inferito come tabella.  
  
-   Gli attributi vengono inferiti come colonne.  
  
-   Gli elementi a cui non sono associati attributi o elementi figlio e che non si ripetono vengono inferiti come colonne.  
  
-   Nel caso di elementi inferiti come tabelle annidate all'interno di altri elementi inferiti a loro volta come tabelle, viene creato un oggetto **DataRelation** annidato tra le due tabelle.  Una nuova colonna di chiave primaria denominata **TableName\_Id** viene aggiunta a entrambe le tabelle e usata dall'oggetto **DataRelation**.  Viene creato un vincolo **ForeignKeyConstraint** tra le due tabelle usando la colonna **TableName\_Id**.  
  
-   Nel caso di elementi inferiti come tabelle e contenenti testo ma privi di elementi figlio, per il testo di ogni elemento viene creata una nuova colonna denominata **TableName\_Text**.  Se un elemento viene inferito come tabella e dispone di testo, ma a tale elemento sono associati anche elementi figlio, il testo verrà ignorato.  
  
## Vedere anche  
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)