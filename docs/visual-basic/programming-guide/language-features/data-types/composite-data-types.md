---
title: "Composite Data Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "classes [Visual Basic], composite data types"
  - "composite types"
  - "composite data types"
  - "data types [Visual Basic], composite"
  - "arrays [Visual Basic], composite data types"
  - "structures, composite data types"
  - "classes [Visual Basic], composite types"
  - "types [Visual Basic], composite"
ms.assetid: 62970f2e-52c0-4369-8963-613820f1f434
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Composite Data Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Oltre ai tipi di dati elementari disponibili in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], è possibile unire elementi di tipo diverso in modo da creare *tipi di dati compositi* quali strutture, matrici e classi.  È possibile compilare tipi di dati compositi utilizzando tipi di base nonché altri tipi compositi.  È ad esempio possibile definire una matrice di elementi struttura o una struttura con membri di tipo matrice.  
  
## Tipi di dati  
 Un tipo composto è differente dal tipo di dati di qualunque suo componente.  Una matrice di elementi `Integer`, ad esempio, non appartiene a sua volta al tipo di dati `Integer`.  
  
 Un tipo di dati matrice viene generalmente rappresentato specificando il tipo dell'elemento, le virgole e le parentesi nel modo appropriato.  Una matrice unidimensionale di elementi `String` viene, ad esempio, rappresentata come `String()` mentre una matrice bidimensionale di elementi `Boolean` viene rappresentata come `Boolean(,)`.  
  
## Tipi di struttura  
 Non esiste alcun tipo di dati singolo che abbracci tutte le strutture.  Piuttosto, ogni definizione di una struttura rappresenta un tipo di dati univoco, anche se due strutture definiscono elementi identici nello stesso ordine.  Se, tuttavia, si creano due o più istanze della stessa struttura, il relativo tipo di dati viene considerato identico in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## Tipi di matrice  
 Non esiste un singolo tipo di dati che abbraccia tutte le matrici.  Il tipo di dati di una particolare istanza di matrice viene determinato da quanto segue:  
  
-   Il fatto di essere una matrice  
  
-   Il numero di dimensioni della matrice  
  
-   Il tipo di elementi della matrice  
  
 In particolare, la lunghezza di una data dimensione non influenza il tipo di dati dell'istanza,  Questa condizione è illustrata nell'esempio che segue.  
  
```  
Dim arrayA( ) As Byte = New Byte(12) {}  
Dim arrayB( ) As Byte = New Byte(100) {}  
Dim arrayC( ) As Short = New Short(100) {}  
Dim arrayD( , ) As Short  
Dim arrayE( , ) As Short = New Short(4, 10) {}  
```  
  
 In questo esempio, le variabili di matrice `arrayA` e `arrayB` vengono considerate dello stesso tipo di dati, ovvero `Byte()`, anche se vengono inizializzate su lunghezze differenti.  Le variabili `arrayB` e `arrayC` non sono dello stesso tipo in quanto presentano tipi di elementi differenti.  Le variabili `arrayC` e `arrayD` non sono dello stesso tipo in quanto presentano un numero di dimensioni differente.  Le variabili `arrayD` e `arrayE` hanno lo stesso tipo, ovvero `Short(,)`, in quanto il numero di dimensioni e i tipi degli elementi corrispondono, anche se `arrayD` non è stata ancora inizializzata.  
  
 Per ulteriori informazioni sulle matrici, vedere [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## Tipi classe  
 Non esiste un singolo tipo di dati che abbraccia tutte le classi.  Sebbene una classe possa ereditare da un'altra classe, ciascuna di esse rappresenta un tipo di dati separato.  Più istanze della stessa classe presentano lo stesso tipo di dati.  Se si assegna una variabile di istanza di una classe a un'altra variabile, esse non solo presentano lo stesso tipo di dati, ma puntano anche alla stessa istanza di classe nella memoria.  
  
 Per ulteriori informazioni sulle classi, vedere [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md).  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [How to: Hold More Than One Value in a Variable](../../../../visual-basic/programming-guide/language-features/data-types/how-to-hold-more-than-one-value-in-a-variable.md)