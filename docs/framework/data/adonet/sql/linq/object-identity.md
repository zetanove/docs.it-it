---
title: "Identit&#224; di oggetti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c788f2f9-65cc-4455-9907-e8388a268e00
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Identit&#224; di oggetti
Gli oggetti in runtime hanno identità univoche.  Se due variabili fanno riferimento allo stesso oggetto, si riferiscono in effetti alla stessa istanza dell'oggetto.  Per questo motivo le modifiche apportate per mezzo di un percorso tramite una variabile sono immediatamente visibili tramite l'altra.  
  
 Le righe in una tabella di database relazionale non hanno identità univoche.  Poiché a ogni riga è associata una chiave primaria univoca, non è possibile che due righe condividano lo stesso valore della chiave.  Questo fatto, tuttavia, limita solo il contenuto della tabella di database.  
  
 In realtà i dati vengono più frequentemente estratti dal database e immessi in un livello diverso dove possono essere usati da un'applicazione.  Questo è il modello supportato da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Quando i dati vengono estratti dal database come righe, non si prevede che due righe che rappresentano gli stessi dati corrispondano in effetti alle stesse istanze della riga.  Se si esegue due volte una query per un cliente specifico, vengono restituite due righe di dati e ogni riga contiene le stesse informazioni.  
  
 Con gli oggetti il comportamento previsto è molto diverso.  Infatti è prevedibile che se viene inviata ripetutamente una richiesta a <xref:System.Data.Linq.DataContext> per ottenere le stesse informazioni, verrà in effetti restituita la stessa istanza dell'oggetto.  Questo comportamento è prevedibile in quanto gli oggetti hanno un significato particolare per l'applicazione ed è implicito che si comportino come oggetti.  Sono infatti stati progettati come gerarchie o grafici,  quindi si deduce che vengano recuperati come tali e non che vengano restituite molteplici istanze replicate solo perché è stata inviata più volte la stessa richiesta.  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] l'identità degli oggetti viene gestita da <xref:System.Data.Linq.DataContext>.  Ogni qualvolta si recupera una nuova riga dal database, la riga viene registrata in una tabella di identità in base alla relativa chiave primaria e viene creato un nuovo oggetto.  Quando si recupera quella riga, viene restituita all'applicazione l'istanza dell'oggetto originale.  In questo modo il concetto di identità riconosciuto dal database, ovvero le chiavi primarie, viene convertito da <xref:System.Data.Linq.DataContext> nel concetto di identità riconosciuto dal linguaggio, ovvero le istanze.  L'oggetto viene visto dall'applicazione nello stato in cui è stato recuperato la prima volta.  I dati nuovi, se diversi, vengono ignorati.  Per altre informazioni, vedere [Recupero di oggetti dalla cache delle identità](../../../../../../docs/framework/data/adonet/sql/linq/retrieving-objects-from-the-identity-cache.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] usa questo approccio per gestire l'integrità degli oggetti locali in modo da supportare gli aggiornamenti ottimistici.  Poiché le uniche modifiche che si verificano dopo la creazione iniziale dell'oggetto sono quelle apportate dall'applicazione, lo scopo dell'applicazione risulta chiaro.  Se nel frattempo sono state apportate modifiche da una parte di un elemento esterno, queste vengono identificate al momento della chiamata a `SubmitChanges()`.  
  
> [!NOTE]
>  Se l'oggetto richiesto dalla query è facilmente identificabile come oggetto già recuperato, la query non viene eseguita.  La tabella di identità funge come una cache di tutti gli oggetti precedentemente recuperati.  
  
## Esempi  
  
### Memorizzazione di oggetti nella cache \- Esempio 1  
 In questo esempio se si esegue la stessa query due volte, viene restituito ogni volta un riferimento allo stesso oggetto in memoria.  
  
 [!code-csharp[DLinqObjectIdentity#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#1)]
 [!code-vb[DLinqObjectIdentity#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#1)]  
  
### Memorizzazione di oggetti nella cache \- Esempio 2  
 In questo esempio se si eseguono query diverse che restituiscono la stessa riga dal database, viene restituito ogni volta un riferimento allo stesso oggetto in memoria.  
  
 [!code-csharp[DLinqObjectIdentity#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#2)]
 [!code-vb[DLinqObjectIdentity#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#2)]  
  
## Vedere anche  
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)