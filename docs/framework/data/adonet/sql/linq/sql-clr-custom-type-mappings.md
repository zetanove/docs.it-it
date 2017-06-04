---
title: "Mapping dei tipi personalizzati SQL-CLR | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d916c7fb-4b56-4214-acbe-5e23365047b2
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Mapping dei tipi personalizzati SQL-CLR
Il mapping dei tipi tra SQL Server e CLR \(Common Language Runtime\) viene specificato automaticamente quando si usa lo strumento da riga di comando SQLMetal o Progettazione relazionale oggetti.  
  
 Quando non viene eseguito alcun mapping personalizzato, questi strumenti assegnano mapping dei tipi predefiniti come descritto in [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md).  Se si desidera usare mapping dei tipi diversi da quelli predefiniti, è necessario personalizzarli.  
  
 Quando si personalizzano i mapping dei tipi, l'approccio consigliato consiste nell'apportare le modifiche in un file DBML intermedio.  Il file DBML personalizzato può quindi essere usato quando si creano i file di codice e di mapping con SQLMetal o Progettazione relazionale oggetti.  
  
 Dopo aver creato un'istanza dell'oggetto <xref:System.Data.Linq.DataContext> dai file di codice e di mapping, tramite il metodo <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=fullName> viene creato un database basato sui mapping dei tipi specificati.  Se non vi sono attributi `type` CLR specificati nei mapping, vengono usati i mapping dei tipi predefiniti.  
  
## Personalizzazione con SQLMetal o Progettazione relazionale oggetti  
 Con SQLMetal e Progettazione relazionale oggetti è possibile creare automaticamente un modello a oggetti che include le informazioni sul mapping dei tipi all'interno o all'esterno del file di codice.  Poiché questi file vengono sovrascritti da SQLMetal o da Progettazione relazionale oggetti ogni volta che si ricreano i mapping, l'approccio consigliato per specificare mapping dei tipi personalizzati consiste nel personalizzare un file DBML.  
  
 Per personalizzare i mapping dei tipi con SQLMetal o con Progettazione relazionale oggetti, generare innanzitutto un file DBML.  Prima di generare il file di codice o di mapping, modificare quindi il file DBML per identificare i mapping dei tipi desiderati.  Con SQLMetal, è necessario modificare manualmente gli attributi `Type` e `DbType` nel file DBML per personalizzare il mapping dei tipi.  Con Progettazione relazionale oggetti, è possibile apportare le modifiche all'interno della finestra di progettazione.  Per altre informazioni sull'utilizzo di Progettazione relazionale oggetti, vedere [LINQ to SQL Tools in Visual Studio](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md).  
  
> [!NOTE]
>  Alcuni mapping dei tipi possono comportare eccezioni di overflow o di perdita di dati durante la conversione da o verso il database.  Analizzare attentamente la matrice del comportamento in fase di esecuzione del mapping dei tipi in [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md) prima di eseguire qualsiasi personalizzazione.  
  
 Affinché le personalizzazioni del mapping dei tipi siano riconosciute da SQLMetal o da Progettazione relazionale oggetti, è necessario assicurarsi che questi strumenti dispongano del percorso al file DBML personalizzato quando si genera il file di codice o il file di mapping esterno.  Sebbene non sia necessario per la personalizzazione del mapping dei tipi, è consigliabile separare sempre le informazioni sul mapping dei tipi dal file di codice e generare il file di mapping dei tipi esterno aggiuntivo.  In questo modo, si garantisce maggiore flessibilità in quanto non è necessaria la ricompilazione del file di codice.  
  
## Incorporamento delle modifiche al database  
 Quando il database viene modificato, è necessario aggiornare il file DBML per riflettere tali modifiche.  Questo può essere effettuato creando un nuovo file DBML e quindi eseguendo di nuovo le personalizzazioni del mapping dei tipi.  In alternativa, è possibile confrontare le differenze tra il nuovo file DBML e il file DBML personalizzato e aggiornare il file DBML personalizzato manualmente per riflettere le modifiche al database.  
  
## Vedere anche  
 [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)   
 [Generazione di codice in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)