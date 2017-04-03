---
title: 'Procedura: Accedere agli argomenti della riga di comando utilizzando foreach (Guida per programmatori C#) |Documentazione Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- command-line arguments [C#]
ms.assetid: 89c3e335-3f5b-4e24-8c5a-b8036561fe8a
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2f0e3bce88beafd45a21773a7b26ffb2bb41215d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-access-command-line-arguments-using-foreach-c-programming-guide"></a>Procedura: accedere agli argomenti della riga di comando utilizzando foreach (Guida per programmatori C#)
Un altro approccio per eseguire l'iterazione della matrice consiste nell'usare l'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md), come illustrato in questo esempio. L'istruzione `foreach` può essere usata per eseguire l'iterazione di una matrice, una classe di raccolte .NET Framework o qualsiasi classe o struct che implementa l'interfaccia <xref:System.Collections.IEnumerable>.  
  
> [!NOTE]
>  Quando si esegue un'applicazione in Visual Studio, è possibile specificare argomenti della riga di comando nella [Pagina Debug, Progettazione progetti](https://docs.microsoft.com/visualstudio/ide/reference/debug-page-project-designer).  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrato come stampare gli argomenti della riga di comando usando `foreach`.  
  
 [!code-cs[csProgGuideMain#10](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-access-command-line-arguments-using-foreach_1.cs)]  
  
 [!code-cs[csProgGuideMain#11](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-access-command-line-arguments-using-foreach_2.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Array>   
 <xref:System.Collections>   
 [Compilazione dalla riga di comando con csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [Main() e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [Procedura: Visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Valori restituiti da Main()](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)
