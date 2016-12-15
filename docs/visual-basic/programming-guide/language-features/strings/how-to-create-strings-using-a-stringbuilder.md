---
title: "How to: Create Strings Using a StringBuilder in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "StringBuilder class"
  - "strings [Visual Basic], using StringBuilder"
ms.assetid: 9c042880-aa16-432e-9ccb-cd00abda9ae3
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Create Strings Using a StringBuilder in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo esempio viene costruita una stringa lunga da diverse stringhe più piccole utilizzando la classe <xref:System.Text.StringBuilder>.  La classe <xref:System.Text.StringBuilder> è più efficiente dell'operatore `&=` per la concatenazione di più stringhe.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creata un'istanza della classe <xref:System.Text.StringBuilder> a cui vengono aggiunte 1.000 stringhe, quindi ne viene restituita la rappresentazione di stringa.  
  
 [!code-vb[VbVbalrStrings#70](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-create-strings-using-a-stringbuilder_1.vb)]  
  
## Vedere anche  
 [Uso della classe StringBuilder](../Topic/Using%20the%20StringBuilder%20Class%20in%20the%20.NET%20Framework.md)   
 [&\= Operator](../../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [Strings](../../../../visual-basic/programming-guide/language-features/strings/index.md)   
 [Creazione di nuove stringhe](../Topic/Creating%20New%20Strings%20in%20the%20.NET%20Framework.md)   
 [Modifica di stringhe](../Topic/Manipulating%20Strings%20in%20the%20.NET%20Framework.md)   
 [Strings Sample](http://msdn.microsoft.com/it-it/be9e82a3-dc95-4aaa-9396-61b66e467e02)