---
title: "Declared Element Characteristics (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declared elements, lifetime"
  - "access levels, declared elements"
  - "declared elements, scope"
  - "visibility, declared elements"
  - "elements, programming"
  - "scope, declared elements"
  - "lifetime, declared elements"
  - "declared elements, access level"
  - "data types [Visual Basic], declared elements"
  - "declared elements, visibility"
ms.assetid: 1bc40fb8-b67c-4428-90a4-76b630ae2583
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Declared Element Characteristics (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una *caratteristica* di un elemento dichiarato è un aspetto dell'elemento che ha effetto sulle modalità di interazione del codice con l'elemento.  A ogni elemento dichiarato è associata una o più caratteristiche tra le seguenti:  
  
-   *Tipo di dati* ovvero i valori che l'elemento può contenere e le relative modalità di archiviazione.  Per ulteriori informazioni, vedere [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
-   *Durata* ovvero il periodo del tempo di esecuzione durante il quale l'elemento è disponibile per l'utilizzo.  Per ulteriori informazioni, vedere [Lifetime in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md).  
  
-   *Ambito* ovvero l'insieme di tutto il codice che può fare riferimento all'elemento senza qualificarne il nome.  Per ulteriori informazioni, vedere [How to: Control the Scope of a Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md).  
  
-   *Livello di accesso* ovvero l'autorizzazione per il codice all'utilizzo dell'elemento.  Per ulteriori informazioni, vedere [How to: Control the Availability of a Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-availability-of-a-variable.md).  
  
## Caratteristiche degli elementi  
 Nella tabella riportata di seguito sono descritti gli elementi dichiarati e le caratteristiche applicabili a ciascuno.  
  
|Elemento|Tipo di dati|Durata|Ambito <sup>1</sup>|Livello di accesso|  
|--------------|------------------|------------|-------------------------|------------------------|  
|Variabile|Sì|Sì|Sì|Sì|  
|Costante|Sì|No|Sì|Sì|  
|Enumerazione|Sì|No|Sì|Sì|  
|Struttura|No|No|Sì|Sì|  
|Proprietà|Sì|Sì|Sì|Sì|  
|Metodo|No|Sì|Sì|Sì|  
|Routine \(`Sub` o `Function`\)|No|Sì|Sì|Sì|  
|Parametro di routine|Sì|Sì|Sì|No|  
|Restituito dalla funzione|Sì|Sì|Sì|No|  
|Operatore|Sì|No|Sì|Sì|  
|Interfaccia|No|No|Sì|Sì|  
|Classe|No|No|Sì|Sì|  
|Evento|No|No|Sì|Sì|  
|Delegato|No|No|Sì|Sì|  
  
 L'ambito <sup>1</sup> è definito talvolta *visibilità*.  
  
## Vedere anche  
 [Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/index.md)   
 [Declared Element Names](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Lifetime in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)