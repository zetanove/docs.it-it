---
title: "Debug di query LINQ to DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4c54015-8ce2-4c5c-8d18-7038144cc66d
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Debug di query LINQ to DataSet
In [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] è supportato il debug di codice [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Vi sono tuttavia alcune differenze tra l'esecuzione del debug di codice [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] e di codice gestito non [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]. La maggior parte delle funzionalità di debug è compatibile con le istruzioni [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], inclusa l'esecuzione di istruzioni, l'impostazione dei punti di interruzione e la visualizzazione dei risultati nelle finestre del debugger.  Tuttavia, l'esecuzione posticipata di query implica tuttavia alcuni effetti collaterali che è necessario tenere in considerazione durante il debug di codice [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] e sono previste alcune limitazioni all'utilizzo di Modifica e continuazione.  In questo argomento vengono illustrati gli aspetti del debug specifici di [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] rispetto al codice gestito non [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  
  
## Visualizzazione dei risultati  
 È possibile visualizzare il risultato di un'istruzione [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] usando i suggerimenti dati, la finestra Espressioni di controllo e la finestra di dialogo Controllo immediato.  Quando si usa una finestra di origine, passare con il puntatore su una query nella finestra di origine per visualizzare un suggerimento dati.  È possibile copiare una variabile [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] e incollarla nella finestra Espressioni di controllo o nella finestra di dialogo Controllo immediato. In [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] le query non vengono valutate al momento della creazione o della dichiarazione, ma solo quando vengono eseguite.  Questo processo è noto come *esecuzione posticipata*.  La variabile della query non dispone pertanto di un valore fino a quando non viene valutata.  Per altre informazioni, vedere [Query in LINQ to DataSet](../../../../docs/framework/data/adonet/queries-in-linq-to-dataset.md).  
  
 Per visualizzare i risultati della query, è necessario che la query venga valutata dal debugger.  Tenere tuttavia presenti alcuni effetti della valutazione implicita, che avviene quando si visualizza il risultato di una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] nel debugger:  La singola valutazione della query  e l'espansione del nodo dei risultati richiedono tempo.  La valutazione ripetuta di alcune query può comportare una notevole riduzione delle prestazioni.  La valutazione di una query può inoltre avere come effetto collaterale la modifica del valore dei dati o dello stato del programma.  Non tutte le query hanno effetti collaterali.  Per determinare la possibilità di valutare una query in modo sicuro, senza effetti collaterali, è necessario conoscere il codice con cui la query viene implementata.  Per altre informazioni, vedere [Espressioni ed effetti secondari](../Topic/Side%20Effects%20and%20Expressions.md).  
  
## Modifica e continuazione  
 In Modifica e continuazione non è supportata la modifica di query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Se si aggiunge, si rimuove o si modificare un'istruzione [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] durante una sessione di debug, viene visualizzata una finestra di dialogo indicante che tale modifica non è supportata da Modifica e continuazione.  A questo punto è possibile annullare la modifica oppure interrompere la sessione di debug per avviare una nuova sessione con il codice modificato.  
  
 In Modifica e continuazione non è supportata neppure la modifica del tipo o del valore delle variabili usate in istruzioni [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Anche in questo caso è possibile annullare le modifiche oppure interrompere e riavviare la sessione di debug.  
  
 In Visual C\# in Visual Studio non è possibile usare Modifica e continuazione su nessun tipo di codice in un metodo contenente una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  
  
 In Visual Basic in Visual Studio, è possibile usare Modifica e continuazione su codice [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] anche in metodi contenente una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  È possibile aggiungere o rimuovere codice prima dell'istruzione [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], anche se le modifiche influiscono sul numero di riga della query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Le modalità di esecuzione del debug Visual Basic di codice [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] rimangono invariate rispetto a prima dell'introduzione di [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Non è tuttavia possibile modificare, aggiungere o rimuovere query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], a meno che non si desideri interrompere il debug per applicare le modifiche.  
  
## Vedere anche  
 [Debug del codice gestito](../Topic/Debugging%20Managed%20Code.md)   
 [Guida per programmatori](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)