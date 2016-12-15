---
title: "Procedura: eseguire l&#39;override del metodo ToString (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "ereditarietà [C#], override di OnPaint e ToString"
  - "ToString (metodo), override in C#"
ms.assetid: 8016db69-1f19-420c-8e17-98e8bebb7749
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: eseguire l&#39;override del metodo ToString (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Ogni classe o struct in C\# eredita in modo implicito la classe <xref:System.Object>.  Ogni oggetto in C\# ottiene pertanto il metodo <xref:System.Object.ToString%2A>, il quale restituisce una rappresentazione in formato stringa di tale oggetto.  Tutte le variabili di tipo `int` dispongono ad esempio di un metodo `ToString`, che consente di restituire il relativo contenuto in formato stringa:  
  
 [!code-cs[csProgGuideInheritance#37](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-override-the-tostring-method_1.cs)]  
  
 Quando si crea una struttura o una classe personalizzata, è necessario eseguire l'override del metodo <xref:System.Object.ToString%2A> per fornire informazioni sul tipo al codice client.  
  
 Per informazioni su come utilizzare le stringhe di formato e altri tipi di formattazioni personalizzate con il metodo di `ToString` , vedere [Formattazione di tipi](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md).  
  
> [!IMPORTANT]
>  Quando si decide quali informazioni fornire attraverso questo metodo, considerare se la classe o la struttura verrà utilizzata da codice non attendibile.  Assicurarsi di non fornire informazioni che potrebbero essere utilizzate da codice dannoso.  
  
### Per eseguire l'override del metodo ToString nella classe o nello struct  
  
1.  Dichiarare un metodo `ToString` con i modificatori e il tipo restituito seguenti:  
  
    ```c#  
    public override string ToString(){}  
    ```  
  
2.  Implementare il metodo in modo che restituisca una stringa.  
  
     Nell'esempio seguente viene restituito il nome della classe insieme ai dati specifici di una determinata istanza della classe.  
  
     [!code-cs[csProgGuideInheritance#36](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-override-the-tostring-method_2.cs)]  
  
     È possibile testare il metodo `ToString` come illustrato nell'esempio di codice seguente:  
  
     [!code-cs[csProgGuideInheritance#38](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-override-the-tostring-method_3.cs)]  
  
## Vedere anche  
 <xref:System.IFormattable>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [string](../../../csharp/language-reference/keywords/string.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [override](../../../csharp/language-reference/keywords/override.md)   
 [virtuale](../../../csharp/language-reference/keywords/virtual.md)   
 [Formattazione di tipi](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md)