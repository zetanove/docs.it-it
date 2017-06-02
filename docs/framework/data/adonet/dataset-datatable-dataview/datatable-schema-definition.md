---
title: "Definizione dello schema di DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efbcdda4-f5a9-421d-8be2-4c194c74552f
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Definizione dello schema di DataTable
Lo schema, o struttura, di una tabella viene rappresentato da colonne e vincoli.  Lo schema di un tipo <xref:System.Data.DataTable> viene definito usando gli oggetti <xref:System.Data.DataColumn> oltre agli oggetti <xref:System.Data.ForeignKeyConstraint> e <xref:System.Data.UniqueConstraint>.  Le colonne di una tabella possono essere associate a colonne di un'origine dati, contenere valori calcolati da espressioni, incrementare automaticamente i propri valori o contenere valori di chiavi primarie.  
  
 I riferimenti basati sui nomi a colonne, relazioni e vincoli di una tabella distinguono tra maiuscole e minuscole.  Pertanto, in una tabella possono coesistere due o più colonne, relazioni o vincoli con lo stesso nome ma che presentano una combinazione diversa di maiuscole e minuscole.  È possibile, ad esempio, che siano presenti sia **Col1** che **col1**.  In tal caso, è necessario che in un riferimento a una delle colonne basato sul nome venga usato il nome con la stessa combinazione di maiuscole e minuscole adottata nella colonna. Se il nome non corrisponde, verrà generata un'eccezione.  Se ad esempio nella tabella **myTable** sono contenute le colonne **Col1** e **col1**, il riferimento basato sul nome a **Col1** sarà **myTable.Columns\["Col1"\]** e il riferimento a **col1** sarà **myTable.Columns\["col1"\]**.  Se si tenta di fare riferimento a una delle due colonne come **myTable.Columns\["COL1"\]**, verrà generata un'eccezione.  
  
 La distinzione tra maiuscole e minuscole non è rilevante se nella tabella è presente solo una colonna, una relazione o un vincolo con un determinato nome.  Ovvero, se nella tabella non sono presenti altre relazioni o oggetti Constraint il cui nome corrisponda al nome della particolare colonna o relazione o oggetto Constraint, è possibile fare riferimento all'oggetto mediante il nome, usando sia lettere maiuscole che minuscole, senza che venga generata alcuna eccezione.  Se ad esempio nella tabella è presente solo **Col1**, è possibile fare riferimento a tale colonna usando **my.Columns\["COL1"\]**.  
  
> [!NOTE]
>  La proprietà <xref:System.Data.DataTable.CaseSensitive%2A> di **DataTable** non influisce su tale comportamento.  Tale proprietà viene infatti applicata ai dati della tabella e influisce sull'ordinamento, la ricerca, l'applicazione di filtri, di vincoli e così via, ma non sui riferimenti a colonne, relazioni e vincoli.  
  
## In questa sezione  
 [Aggiunta di colonne a un DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-columns-to-a-datatable.md)  
 Viene descritta la definizione delle colonne di una tabella tramite gli oggetti **DataColumn**.  
  
 [Creazione di colonne di espressioni](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-expression-columns.md)  
 Viene spiegato come usare la proprietà **Expression** di una colonna per calcolare valori basati sui valori di altre colonne della riga.  
  
 [Creazione di colonne AutoIncrement](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-autoincrement-columns.md)  
 Viene descritto come impostare una colonna in modo che incrementi automaticamente i valori numerici, per garantire un valore di colonna univoco per ogni riga.  
  
 [Definizione di chiavi primarie](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md)  
 Viene descritto come specificare la chiave primaria di una tabella da uno o più oggetti **DataColumn**.  
  
 [Vincoli di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)  
 Viene descritto come definire vincoli di chiave esterna e univoci per le colonne di una tabella.  
  
## Vedere anche  
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)