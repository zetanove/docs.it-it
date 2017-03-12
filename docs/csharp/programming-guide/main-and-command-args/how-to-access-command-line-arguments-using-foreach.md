---
title: "Procedura: accedere agli argomenti della riga di comando utilizzando foreach (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "argomenti della riga di comando [C#]"
ms.assetid: 89c3e335-3f5b-4e24-8c5a-b8036561fe8a
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Procedura: accedere agli argomenti della riga di comando utilizzando foreach (Guida per programmatori C#)
Per scorrere gli elementi di una matrice, è anche possibile utilizzare l'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md), come mostrato in questo esempio.  L'istruzione `foreach` consente di scorrere gli elementi di una matrice, di una classe Collection .NET Framework o di qualsiasi classe o struttura che implementa l'interfaccia <xref:System.Collections.IEnumerable>.  
  
> [!NOTE]
>  Quando si esegue un'applicazione in Visual Studio, è possibile specificare gli argomenti della riga di comando nella [Pagina Debug, Progettazione progetti](/visual-studio/ide/reference/debug-page-project-designer).  
  
## Esempio  
 In questo esempio viene illustrato come stampare gli argomenti della riga di comando utilizzando `foreach`.  
  
 [!code-cs[csProgGuideMain#10](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/how-to-access-command-li_1.cs)]  
  
 [!code-cs[csProgGuideMain#11](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/how-to-access-command-li_2.cs)]  
  
## Vedere anche  
 <xref:System.Array>   
 <xref:System.Collections>   
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [Main\(\) e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [Procedura: visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Valori restituiti da Main\(\)](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)