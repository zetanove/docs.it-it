---
title: "Formulare proiezioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 745742df-0eda-479b-83f8-29bd8a80db96
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Formulare proiezioni
Negli esempi seguenti viene illustrato come è possibile combinare l'istruzione `select` in C\# e l'istruzione `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] con altre funzionalità per formare proiezioni della query.  
  
## Esempio  
 Nell'esempio seguente viene usata la clausola `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)], ovvero la clausola `select` in C\#, per restituire una sequenza di nomi di contatti per `Customers`.  
  
 [!code-csharp[DLinqQueryExamples#57](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#57)]
 [!code-vb[DLinqQueryExamples#57](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#57)]  
  
## Esempio  
 Nell'esempio seguente viene usata la clausola `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)], ovvero la clausola `select` in C\#, e *tipi anonimi* per restituire una sequenza di nomi di contatti e numeri di telefono per `Customers`.  
  
 [!code-csharp[DLinqQueryExamples#58](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#58)]
 [!code-vb[DLinqQueryExamples#58](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#58)]  
  
## Esempio  
 Nell'esempio seguente viene usata la clausola `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)], ovvero la clausola `select` in C\#, e *tipi anonimi* per restituire una sequenza di nomi e numeri di telefono per i dipendenti.  I campi `FirstName` e `LastName` vengono combinati in un unico campo \(`Name`\) e il campo `HomePhone` viene rinominato in `Phone` nella sequenza risultante.  
  
 [!code-csharp[DLinqQueryExamples#59](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#59)]
 [!code-vb[DLinqQueryExamples#59](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#59)]  
  
## Esempio  
 Nell'esempio seguente viene usata la clausola `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)], ovvero la clausola `select` in C\#, e *tipi anonimi* per restituire una sequenza di tutte le voci presenti in `ProductID` e un valore calcolato denominato `HalfPrice`.  Questo valore viene impostato su `UnitPrice` e diviso per 2.  
  
 [!code-csharp[DLinqQueryExamples#60](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#60)]
 [!code-vb[DLinqQueryExamples#60](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#60)]  
  
## Esempio  
 Nell'esempio seguente viene usata la clausola `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)], ovvero la clausola `select` in C\#, e un'*istruzione condizionale* per restituire una sequenza di nome di prodotto e disponibilità del prodotto.  
  
 [!code-csharp[DLinqQueryExamples#61](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#61)]
 [!code-vb[DLinqQueryExamples#61](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#61)]  
  
## Esempio  
 Nell'esempio seguente viene usata una clausola [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] `Select`, ovvero una clausola `select` in C\#, e un *tipo conosciuto* \(Name\) per restituire una sequenza di nomi di dipendenti.  
  
 [!code-csharp[DLinqQueryExamples#62](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#62)]
 [!code-vb[DLinqQueryExamples#62](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#62)]  
  
## Esempio  
 Nell'esempio seguente vengono usati `Select` e `Where` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)], ovvero `select` e `where` in C\#, per restituire una *sequenza filtrata* di nomi di contatti per i clienti nell'area londinese.  
  
 [!code-csharp[DLinqQueryExamples#63](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#63)]
 [!code-vb[DLinqQueryExamples#63](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#63)]  
  
## Esempio  
 Nell'esempio seguente viene usata una clausola `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)], ovvero una clausola `select` in C\#, e *tipi anonimi* per restituire un *subset con shaping* dei dati sui clienti.  
  
 [!code-csharp[DLinqQueryExamples#64](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#64)]
 [!code-vb[DLinqQueryExamples#64](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#64)]  
  
## Esempio  
 Nell'esempio seguente vengono usate query annidate per restituire i risultati riportati di seguito:  
  
-   Una sequenza di tutti gli ordini e dei corrispondenti `OrderID`.  
  
-   Una sottosequenza degli elementi nell'ordine per cui è presente uno sconto.  
  
-   L'importo risparmiato se il costo di spedizione non è incluso.  
  
 [!code-csharp[DLinqQueryExamples#65](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#65)]
 [!code-vb[DLinqQueryExamples#65](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#65)]  
  
## Vedere anche  
 [Esempi di query](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)