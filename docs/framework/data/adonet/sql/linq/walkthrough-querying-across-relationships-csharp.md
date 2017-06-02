---
title: "Procedura dettagliata: query tra relazioni (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 552abeb1-18f2-4e93-a9c6-ef7b2db30c32
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura dettagliata: query tra relazioni (C#)
In questa procedura dettagliata viene descritto l'uso delle *associazioni* [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per rappresentare relazioni di chiave esterna nel database.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Questa procedura è stata scritta usando Impostazioni di sviluppo di Visual C\#.  
  
## Prerequisiti  
 È necessario avere completato la [Procedura dettagliata: modello a oggetti e query semplici \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-csharp.md).  Questa procedura dettagliata si basa su tale procedura dettagliata, inclusa la presenza del file northwnd.mdf in c:\\linqtest5.  
  
## Panoramica  
 La procedura dettagliata è costituita da tre attività principali:  
  
-   Aggiunta di una classe di entità per rappresentare la tabella Orders nel database di esempio Northwind.  
  
-   Completamento delle annotazioni alla classe `Customer` per migliorare la relazione tra le classi `Customer` e `Order`.  
  
-   Creazione ed esecuzione di una query per testare la capacità di ottenere informazioni su `Order` usando la classe `Customer`.  
  
## Esecuzione del mapping delle relazioni tra tabelle  
 Dopo la definizione della classe `Customer`, creare la definizione della classe di entità `Order` includendo il codice seguente per indicare che `Order.Customer` è correlata come chiave esterna a `Customer.CustomerID`.  
  
#### Per aggiungere la classe di entità Order  
  
-   Digitare o incollare il codice seguente dopo la classe `Customer`:  
  
     [!code-csharp[DLinqWalk2CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#1)]  
  
## Annotazione della classe Customer  
 In questo passaggio vengono aggiunte annotazioni alla classe `Customer` per indicare la relazione alla classe `Order`.  Questa aggiunta non è strettamente necessaria, in quanto la definizione della relazione in una direzione è sufficiente per creare il collegamento.  Tuttavia aggiungendo l'annotazione sarà possibile spostarsi facilmente tra gli oggetti in entrambe le direzioni.  
  
#### Per annotare la classe Customer  
  
-   Digitare o incollare il codice seguente nella classe `Customer`:  
  
     [!code-csharp[DLinqWalk2CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#2)]  
  
## Creazione ed esecuzione di un query sulla relazione Customer\-Order  
 A questo punto è possibile accedere direttamente agli oggetti `Order` dagli oggetti `Customer` o viceversa.  Non è necessario creare un *join* esplicito tra clienti e ordini.  
  
#### Per accedere agli oggetti Order usando oggetti Customer  
  
1.  Modificare il metodo `Main` digitando o incollando il codice seguente nel metodo stesso:  
  
     [!code-csharp[DLinqWalk2CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#3)]  
  
2.  Premere F5 per eseguire il debug dell'applicazione.  
  
    > [!NOTE]
    >  È possibile eliminare il codice SQL nella finestra della console impostando come commento `db.Log = Console.Out;`.  
  
3.  Premere INVIO nella finestra della console per terminare il debug.  
  
## Creazione di una visualizzazione fortemente tipizzata del database  
 È molto più facile iniziare con una visualizzazione fortemente tipizzata del database.  Applicando la tipizzazione forte all'oggetto <xref:System.Data.Linq.DataContext>, si eviterà di eseguire chiamate a <xref:System.Data.Linq.DataContext.GetTable%2A>.  Quando si usa l'oggetto fortemente tipizzato <xref:System.Data.Linq.DataContext>, è possibile usare tabelle fortemente tipizzate in tutte le query.  
  
 Nei passaggi seguenti si creerà `Customers` come tabella fortemente tipizzata mappata alla tabella Customers nel database.  
  
#### Per tipizzare fortemente l'oggetto DataContext  
  
1.  Aggiungere il codice riportato di seguito sopra la dichiarazione della classe `Customer`.  
  
     [!code-csharp[DLinqWalk2CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#4)]  
  
2.  Per usare l'oggetto fortemente tipizzato <xref:System.Data.Linq.DataContext>, modificare il metodo `Main` come segue:  
  
     [!code-csharp[DLinqWalk2CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#5)]  
  
3.  Premere F5 per eseguire il debug dell'applicazione.  
  
     L'output nella finestra della console sarà:  
  
     `ID=WHITC`  
  
4.  Premere INVIO nella finestra della console per terminare il debug.  
  
## Passaggi successivi  
 Nella successiva procedura dettagliata, [Procedura dettagliata: modifica dei dati \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-csharp.md), verrà illustrato come modificare i dati.  Per tale procedura dettagliata non è necessario avere salvato le due procedure dettagliate di questa serie già completate.  
  
## Vedere anche  
 [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)