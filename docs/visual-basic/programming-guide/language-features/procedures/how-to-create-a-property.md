---
title: "How to: Create a Property (Visual Basic) | Microsoft Docs"
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
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "Visual Basic code, properties"
  - "properties [Visual Basic]"
ms.assetid: 4d229712-6be8-4c5c-bac5-06995ce9185a
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Create a Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una definizione di proprietà viene racchiusa tra un'istruzione `Property` e un'istruzione `End Property`.  All'interno della definizione è necessario definire una routine `Get`, una routine `Set` o entrambe.  Tra le due routine è incluso tutto il codice della proprietà.  
  
 La routine `Get` recupera il valore della proprietà, mentre la routine `Set` memorizza un valore.  Per assegnare alla proprietà l'accesso in lettura e in scrittura, è necessario definire entrambe le routine.  Per una proprietà di sola lettura viene definita soltanto la routine `Get`, mentre per una proprietà di sola scrittura viene definita soltanto la routine `Set`.  
  
### Per creare una proprietà  
  
1.  All'esterno di qualsiasi proprietà o routine utilizzare un'[Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md), seguita da un'istruzione `End Property`.  
  
2.  Se la proprietà accetta parametri, dopo la parola chiave `Property` inserire il nome della routine, quindi l'elenco dei parametri tra parentesi.  
  
3.  Dopo le parentesi inserire una clausola `As` per specificare il tipo di dati del valore della proprietà.  È necessario specificare il tipo di dati anche per una proprietà di sola scrittura.  
  
4.  Aggiungere le routine `Get` e `Set` nel modo appropriato.  Vedere le istruzioni riportate di seguito.  
  
### Per creare una routine Get che recupera il valore di una proprietà  
  
1.  Tra le istruzioni `Property` ed `End Property` definire un'[Get Statement](../../../../visual-basic/language-reference/statements/get-statement.md), seguita da un'istruzione `End Get`.  Per la routine `Get` non è necessario definire alcun parametro.  
  
2.  Inserire le istruzioni del codice necessarie per il recupero del valore della proprietà tra le istruzioni `Get` ed `End Get`.  Oltre a generare e restituire il valore della proprietà, il codice può includere altri calcoli e modifiche di dati.  
  
3.  Utilizzare un'istruzione `Return` per restituire il valore della proprietà al codice chiamante.  
  
 È necessario definire una routine `Get` sia per una proprietà di lettura e scrittura che per una proprietà di sola lettura.  Non deve invece essere definita una routine `Get` per una proprietà di sola scrittura.  
  
### Per creare una routine Set che definisce il valore di una proprietà  
  
1.  Tra le istruzioni `Property` ed `End Property` definire un'[Set Statement](../../../../visual-basic/language-reference/statements/set-statement.md), seguita da un'istruzione `End Set`.  
  
2.  All'interno dell'istruzione `Set` inserire un elenco di parametri tra parentesi dopo la parola chiave `Set`.  Tale elenco deve includere almeno un parametro specifico per il valore passato dal codice chiamante.  Il nome predefinito per questo parametro è `Value`, ma è possibile utilizzare un nome diverso in base alle esigenze.  Il tipo di dati del parametro valore deve corrispondere a quello della proprietà stessa.  
  
3.  Inserire le istruzioni del codice necessarie per la memorizzazione di un valore nella proprietà tra le istruzioni `Set` ed `End Set`.  Oltre a convalidare e memorizzare il valore della proprietà, il codice può includere altri calcoli e modifiche di dati.  
  
4.  Utilizzare il parametro valore per accettare il valore fornito dal codice chiamante.  Il valore può essere memorizzato direttamente in un'istruzione di assegnazione oppure utilizzato in un'espressione per il calcolo del valore interno da memorizzare.  
  
 È necessario definire una routine `Set` sia per una proprietà di lettura e scrittura che per una proprietà di sola scrittura.  Non deve invece essere definita una routine `Set` per una proprietà di sola lettura.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creata una proprietà di lettura e scrittura che memorizza un nome completo costituito da due parti, ossia il nome e il cognome.  Quando il codice chiamante legge `fullName`, la routine `Get` combina le due parti costitutive e restituisce il nome completo.  Quando il codice chiamante assegna un nuovo nome completo, la routine `Set` tenta di scomporlo in due parti costitutive.  Se non viene rilevato alcuno spazio, viene memorizzato tutto come nome.  
  
 [!code-vb[VbVbcnProcedures#8](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-create-a-property_1.vb)]  
  
 Nell'esempio riportato di seguito vengono illustrate le chiamate tipiche alle routine delle proprietà di `fullName`.  La prima chiamata imposta il valore delle proprietà, mentre la seconda lo recupera.  
  
 [!code-vb[VbVbcnProcedures#9](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-create-a-property_2.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [How to: Call a Property Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [How to: Put a Value in a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [How to: Get a Value from a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)