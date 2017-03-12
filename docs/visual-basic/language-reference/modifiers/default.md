---
title: "Default (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Default"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "defaults, properties"
  - "properties [Visual Basic], default"
  - "default properties, in Visual Basic"
  - "Default keyword [Visual Basic]"
  - "default properties"
ms.assetid: 45fce9b9-d212-4b2d-ab86-6e359b8b57af
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Default (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Identifica una proprietà come proprietà predefinita della classe, struttura o interfaccia corrispondente.  
  
## Note  
 Per una classe, una struttura o un'interfaccia è possibile designare al massimo una delle rispettive proprietà come *proprietà predefinita*, purché questa accetti almeno un parametro.  Se il codice fa riferimento a una classe o a una struttura senza specificare un membro, il riferimento viene risolto nella proprietà predefinita.  
  
 L'utilizzo di proprietà predefinite può consentire una lieve riduzione del numero di caratteri del codice sorgente, ma può rendere più difficile la lettura di tale codice.  Se il codice chiamante non viene comunemente utilizzato con una specifica classe o struttura, quando fa riferimento al nome di quest'ultima non è in grado di determinare se il riferimento accede alla classe o alla struttura oppure a una proprietà predefinita.  Questa situazione può generare errori del compilatore o errori meno evidenti della logica di runtime.  
  
 È possibile ridurre in qualche misura il rischio di errori generati dalla proprietà predefinita utilizzando sempre l'[Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md) per impostare il controllo dei tipi del compilatore su `On`.  
  
 Se si intende utilizzare una classe o una struttura predefinita nel codice, è necessario stabilire se include una proprietà predefinita e, in caso affermativo, identificarne il nome.  
  
 A causa degli svantaggi elencati, si consiglia di evitare di specificare proprietà predefinite.  Per migliorare la leggibilità del codice, si consiglia inoltre di fare sempre riferimento in modo esplicito a tutte le proprietà, incluse quelle predefinite.  
  
 È possibile utilizzare il modificatore `Default` nel seguente contesto:  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## Vedere anche  
 [How to: Declare and Call a Default Property in Visual Basic](../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)