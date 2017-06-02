---
title: "DataSet tipizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 033d2548-cf24-4c05-8179-67d8b009c048
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataSet tipizzati
Oltre all'accesso ad associazione tardiva ai valori tramite variabili tipizzate in modo debole, nel tipo <xref:System.Data.DataSet> è disponibile l'accesso ai dati tramite una metafora tipizzata in modo sicuro.  È possibile accedere alle tabelle e alle colonne che fanno parte del **DataSet** usando nomi descrittivi e variabili tipizzate in modo sicuro.  
  
 Un **DataSet** tipizzato è una classe derivata da un **DataSet**.  In quanto tale, eredita tutti i metodi, gli eventi e le proprietà di un **DataSet**.  Un **DataSet** tipizzato fornisce inoltre metodi, eventi e proprietà tipizzati in modo sicuro.  È quindi possibile accedere mediante il nome alle tabelle e alle colonne, invece di usare metodi basati sulle raccolte.  Oltre a consentire una migliore leggibilità del codice, un **DataSet** tipizzato consente all'editor del codice di Visual Studio .NET di completare automaticamente le righe digitate.  
  
 Il **DataSet** tipizzato in modo sicuro fornisce inoltre l'accesso a valori come il tipo corretto in fase di compilazione.  Se si usa un **DataSet** tipizzato in modo sicuro, gli errori di mancata corrispondenza del tipo vengono rilevati in fase di compilazione del codice, anziché in fase di esecuzione.  
  
## In questa sezione  
 [Generazione di DataSet fortemente tipizzati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-strongly-typed-datasets.md)  
 Viene descritta la creazione e l'uso di un **DataSet** tipizzato in modo sicuro.  
  
 [Inserimento di annotazioni in DataSet tipizzati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/annotating-typed-datasets.md)  
 Viene descritto come inserire annotazioni nello schema XSD \(XML Schema Definition Language\) usato per generare un **DataSet** tipizzato in modo sicuro per assegnare agli elementi del **DataSet** dei nomi descrittivi, senza alterare lo schema sottostante.  
  
## Vedere anche  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)