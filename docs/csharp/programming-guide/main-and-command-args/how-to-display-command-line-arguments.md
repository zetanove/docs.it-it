---
title: 'Procedura: Visualizzare gli argomenti della riga di comando (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- command-line arguments [C#], displaying
ms.assetid: b8479f2d-9e05-4d38-82da-2e61246e5437
caps.latest.revision: 19
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
ms.openlocfilehash: e46860ecc2f5062abb440a764443ecee19c5153d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-display-command-line-arguments-c-programming-guide"></a>Procedura: visualizzare gli argomenti della riga di comando (Guida per programmatori C#)
Gli argomenti specificati per un file eseguibile dalla riga di comando sono accessibili tramite un parametro facoltativo per `Main`. Gli argomenti vengono specificati sotto forma di una matrice di stringhe. Ogni elemento della matrice contiene un solo argomento. Gli spazi vuoti tra gli argomenti vengono rimossi. Si considerino ad esempio le chiamate seguenti della riga di comando di un file eseguibile fittizio:  
  
|Input riga di comando|Matrice di stringhe passate a Main|  
|----------------------------|-------------------------------------|  
|**executable.exe a b c**|"a"<br /><br /> "b"<br /><br /> "c"|  
|**executable.exe one two**|"one"<br /><br /> "two"|  
|**executable.exe "one two" three**|"one two"<br /><br /> "three"|  
  
> [!NOTE]
>  Quando si esegue un'applicazione in Visual Studio, è possibile specificare argomenti della riga di comando nella [Pagina Debug, Progettazione progetti](https://docs.microsoft.com/visualstudio/ide/reference/debug-page-project-designer).  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono visualizzati gli argomenti della riga di comando passati a un'applicazione della riga di comando. L'output visualizzato è per la prima voce nella tabella precedente.  
  
 [!code-cs[csProgGuideMain#9](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-display-command-line-arguments_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Compilazione dalla riga di comando con csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Main() e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [Procedura: Accedere agli argomenti della riga di comando usando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Valori restituiti da Main()](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)
