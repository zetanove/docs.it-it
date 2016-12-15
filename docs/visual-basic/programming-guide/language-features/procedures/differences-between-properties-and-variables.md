---
title: "Differences Between Properties and Variables in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "property values"
  - "variables [Visual Basic]"
  - "Visual Basic code, procedures"
  - "values, properties"
  - "variables [Visual Basic], definition"
  - "Visual Basic code, variables"
  - "Visual Basic code, properties"
  - "properties [Visual Basic], values"
  - "properties [Visual Basic], defined"
  - "variables [Visual Basic], and properties"
  - "properties [Visual Basic], and variables"
ms.assetid: 7a03a8be-5381-431f-bd7c-16e887e4e07b
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Differences Between Properties and Variables in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Sia le variabili che le proprietà rappresentano valori accessibili.  Vi sono tuttavia differenze nell'ambito della memoria e dell'implementazione.  
  
## Variabili.  
 Una *variabile* corrisponde direttamente a una posizione di memoria  e viene definita mediante una singola istruzione di dichiarazione.  Può essere una *variabile locale*, definita in una routine e disponibile solo all'interno di questa, oppure una *variabile membro*, definita in un modulo, in una classe o in una struttura ma non all'interno di una routine.  Una variabile membro è definita anche *campo*.  
  
## Proprietà  
 Una *proprietà* è un elemento dati definito in un modulo, in una classe o in una struttura.  Per definirla viene utilizzato un blocco di codice tra le istruzioni `Property` e `End Property`.  Tale blocco contiene una routine `Get`, una routine `Set` o entrambe le routine.  Queste ultime sono chiamate *routine delle proprietà* o *funzioni di accesso alle proprietà*.  Oltre al recupero o alla memorizzazione del valore delle proprietà, possono anche consentire l'esecuzione di azioni personalizzate, come l'aggiornamento di un contatore degli accessi.  
  
## Differenze  
 Nella tabella riportata di seguito sono illustrate alcune differenze importanti tra variabili e proprietà.  
  
|Elementi di differenza|Variabile|Proprietà|  
|----------------------------|---------------|---------------|  
|Dichiarazione|Singola istruzione di dichiarazione|Serie di istruzioni in un blocco di codice|  
|Implementazione|Singolo percorso di memoria|Codice eseguibile \(routine delle proprietà\)|  
|Memoria|Direttamente associata al valore della variabile|Generalmente la memoria interna non è disponibile all'esterno del modulo o della classe che contiene la proprietà<br /><br /> Il valore della proprietà può o meno essere disponibile come elemento memorizzato <sup>1</sup>|  
|Codice eseguibile|Nessuno|Deve disporre di almeno una routine|  
|Accesso in lettura e scrittura|Lettura\/scrittura o solo lettura|Lettura\/scrittura, solo lettura o solo scrittura|  
|Azioni personalizzate \(oltre all'accettazione o restituzione di un valore\)|Non consentite|Possono essere eseguite durante l'impostazione o il recupero del valore della proprietà|  
  
 <sup>1</sup> Diversamente da una variabile, il valore di una proprietà potrebbe non corrispondere direttamente a un singolo elemento memorizzato.  È possibile suddividere la memoria in più parti per motivi di praticità o sicurezza oppure memorizzare il valore in un formato crittografato.  In questi casi, la routine `Get` assemblerebbe le parti o decrittograferebbe il valore memorizzato e la routine `Set` crittograferebbe un nuovo valore o lo suddividerebbe nella memoria costitutiva.  Un valore di proprietà può essere effimero, come l'ora del giorno, e in questo caso la routine `Get` lo calcolerebbe immediatamente a ogni accesso alla proprietà.  
  
## Vedere anche  
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [How to: Create a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [How to: Call a Property Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [How to: Put a Value in a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [How to: Get a Value from a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)