---
title: "How to: Create an Add Extension Method Used by a Collection Initializer (Visual Basic) | Microsoft Docs"
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
  - "collection initializers [Visual Basic]"
ms.assetid: f64b52c7-8b11-4410-93a6-cb3aeebcc772
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# How to: Create an Add Extension Method Used by a Collection Initializer (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando si utilizza un inizializzatore di raccolta per creare una raccolta, il compilatore Visual Basic cerca un metodo `Add` del tipo di raccolta per il quale i parametri per il metodo `Add` corrispondono ai tipi dei valori nell'inizializzatore di raccolta.  Questo metodo `Add` viene utilizzato per popolare la raccolta con i valori dell'inizializzatore di raccolta.  
  
 Se non esiste alcun metodo `Add` corrispondente e non è possibile modificare il codice per la raccolta, è possibile aggiungere un metodo di estensione chiamato `Add` che accetta i parametri richiesti dall'inizializzatore di raccolta.  Questa operazione è in genere necessaria quando si utilizzano gli inizializzatori di raccolta per le raccolte generiche.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come aggiungere un metodo di estensione al tipo generico <xref:System.Collections.Generic.List%601> in modo che sia possibile utilizzare un inizializzatore di raccolta per aggiungere oggetti di tipo `Employee`.  Il metodo di estensione consente di utilizzare la sintassi abbreviata dell'inizializzatore di raccolta.  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#1](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/visualbasic/how-to-create-an-add-ext_1.vb)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#2](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/visualbasic/how-to-create-an-add-ext_2.vb)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#3](../../../../visual-basic/programming-guide/language-features/collection-initializers/codesnippet/visualbasic/how-to-create-an-add-ext_3.vb)]  
  
## Vedere anche  
 [Collection Initializers](../../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [How to: Create a Collection Used by a Collection Initializer](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md)