---
title: "Generics e matrici (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici [C#], generics"
  - "generics [C#], matrici"
ms.assetid: 7d956536-3851-41b5-94ad-3e7c0a5fe485
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Generics e matrici (Guida per programmatori C#)
In C\# 2.0 e versioni successive le matrici unidimensionali con un limite inferiore pari a zero implementano automaticamente <xref:System.Collections.Generic.IList%601>.  In questo modo, è possibile creare metodi generici in grado di utilizzare lo stesso codice per scorrere le matrici e altri tipi di di raccolte.  Questa tecnica risulta particolarmente utile per la lettura dei dati nelle raccolte.  Non è possibile utilizzare l'interfaccia <xref:System.Collections.Generic.IList%601> per aggiungere o rimuovere elementi da una matrice.  Se si tenta di chiamare un metodo <xref:System.Collections.Generic.IList%601>, ad esempio <xref:System.Collections.Generic.IList%601.RemoveAt%2A>, su una matrice in questo contesto, viene generata un'eccezione.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come un singolo metodo generico che accetta un parametro di input <xref:System.Collections.Generic.IList%601> può scorrere un elenco e una matrice, in questo caso una matrice di numeri interi.  
  
 [!code-cs[csProgGuideGenerics#35](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-and-arrays_1.cs)]  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Generics](../../../csharp/programming-guide/generics/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Generics](../Topic/Generics%20in%20the%20.NET%20Framework.md)