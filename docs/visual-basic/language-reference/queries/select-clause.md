---
title: "Select Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QuerySelect"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Select statement"
  - "Select clause"
  - "queries [Visual Basic], Select"
ms.assetid: 27a3f61c-5960-4692-9b91-4d0c4b6178fe
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Select Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Definisce il risultato di una query.  
  
## Sintassi  
  
```  
Select [ var1 = ] fieldName1 [, [ var2 = ] fieldName2 [...] ]  
```  
  
## Parti  
 `var1`  
 Parametro facoltativo.  Alias che può essere utilizzato per fare riferimento ai risultati dell'espressione di colonna.  
  
 `fieldName1`  
 Obbligatorio.  Nome del campo da restituire nel risultato della query.  
  
## Note  
 È possibile utilizzare la clausola `Select` per definire i risultati restituibili da una query.  Questo permette di definire i membri di un nuovo tipo anonimo creato da una query, oppure di fare riferimento ai membri di un tipo denominato restituito da una query.  La clausola `Select` non è obbligatoria per una query.  Se non è specificata alcuna clausola `Select`, la query restituirà un tipo basato su tutti i membri delle variabili di intervallo identificate per l'ambito corrente.  Per ulteriori informazioni, vedere [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  Quando una query crea un tipo nominato, restituirà un risultato di tipo <xref:System.Collections.Generic.IEnumerable%601> dove `T` è il tipo creato.  
  
 La clausola `Select` può fare riferimento a qualsiasi variabile nell'ambito corrente.  Sono incluse le variabili di intervallo identificate nella clausola `From` o nelle clausole `From`.  Sono incluse anche tutte le nuove variabili create con un alias dalle clausole `Aggregate`, `Let`, `Group By` o `Group Join` oppure le variabili create da una clausola `Select` precedente nell'espressione di query.  La clausola `Select` può includere anche valori statici.  Nell'esempio di codice seguente viene illustrata un'espressione di query in cui la clausola `Select` definisce il risultato della query come nuovo tipo anonimo con quattro membri: `ProductName`, `Price`, `Discount` e `DiscountedPrice`.  I valori dei membri `ProductName` e `Price` vengono ottenuti dalla variabile di intervallo del prodotto definita nella clausola `From`.  Il valore del membro `DiscountedPrice` viene calcolato nella clausola `Let`.  Il membro `Discount` è un valore statico.  
  
 [!code-vb[VbSimpleQuerySamples#27](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_1.vb)]  
  
 La clausola `Select` introduce un nuovo insieme di variabili di intervallo per le successive clausole della query e le precedenti variabili di intervallo non sono più in ambito.  L'ultima clausola `Select` in un'espressione di query determina il valore restituito della query.  Ad esempio, la query seguente restituisce il nome della società e l'ID ordine per ogni ordine del cliente per il quale il totale supera 500.  La prima clausola `Select` identifica le variabili di intervallo per la clausola `Where` e per la seconda clausola `Select`.  La seconda clausola `Select` identifica i valori restituiti dalla query come nuovo tipo anonimo.  
  
 [!code-vb[VbSimpleQuerySamples#28](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_2.vb)]  
  
 Se la clausola `Select` identifica un solo elemento da restituire, l'espressione di query restituisce una raccolta del tipo di quell'unico elemento.  Se la clausola `Select` identifica più elementi da restituire, l'espressione di query restituisce una raccolta di un nuovo tipo anonimo, basato sugli elementi selezionati.  Ad esempio, nelle due query seguenti sono restituite raccolte di due tipi diversi basati sulla clausola `Select`.  La prima query restituisce una raccolta di nomi di azienda come stringhe.  La seconda query restituisce una raccolta di oggetti `Customer` popolata con i nomi di azienda e le informazioni relative all'indirizzo.  
  
 [!code-vb[VbSimpleQuerySamples#29](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_3.vb)]  
  
## Esempio  
 Nell'espressione di query seguente viene utilizzata una clausola `From` per dichiarare una variabile di intervallo `cust` per la raccolta `customers`.  La clausola `Select` seleziona il nome del cliente e valore ID e popola le colonne `CompanyName` e `CustomerID` della nuova variabile di intervallo.  L'istruzione `For Each` esegue un ciclo per ogni oggetto restituito e visualizza le colonne `CompanyName` e `CustomerID` per ogni record.  
  
 [!code-vb[VbSimpleQuerySamples#30](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_4.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Order By Clause](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)