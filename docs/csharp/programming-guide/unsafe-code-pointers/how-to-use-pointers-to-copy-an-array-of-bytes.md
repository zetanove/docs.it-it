---
title: "Procedura: utilizzare puntatori per copiare una matrice di byte (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici [C#], byte"
  - "matrici di byte [C#]"
  - "puntatori [C#], per copiare byte"
ms.assetid: ec16fbb4-a24e-45f5-a763-9499d3fabe0a
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# Procedura: utilizzare puntatori per copiare una matrice di byte (Guida per programmatori C#)
Nell'esempio seguente vengono utilizzati puntatori per copiare byte da una matrice a un'altra.  
  
 Nell'esempio viene utilizzata la parola chiave [unsafe](../../../csharp/language-reference/keywords/unsafe.md), che consente l'utilizzo di puntatori all'interno del metodo `Copy`.  Per dichiarare i puntatori nelle matrici di origine e destinazione, viene utilizzata l'istruzione [fixed](../../../csharp/language-reference/keywords/fixed-statement.md) che *blocca* la posizione delle matrici di origine e destinazione nella memoria in modo che non vengano rimossi da Garbage Collection.  I blocchi di memoria per le matrici vengono sbloccati quando il blocco `fixed` è completato.  Poiché il metodo `Copy` in questo esempio utilizza la parola chiave `unsafe`, deve essere compilato con l'opzione del compilatore **\/unsafe**.  Per impostare l'opzione in Visual Studio, fare clic con il pulsante destro del mouse sul nome del progetto e quindi scegliere **Proprietà**.  Nella scheda **Compilazione**, selezionare **Consenti codice di tipo unsafe**.  
  
## Esempio  
 [!code-cs[csProgGuidePointers#3](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers2.cs#3)]  
  
 [!code-cs[csProgGuidePointers#18](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#18)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [\/unsafe \(Enable Unsafe Mode\)](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)   
 [Garbage Collection](../Topic/Garbage%20Collection.md)