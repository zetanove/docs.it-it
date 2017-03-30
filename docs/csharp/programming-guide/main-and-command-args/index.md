---
title: Main() e argomenti della riga di comando (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- CS5001
- main_CSharpKeyword
- Main
dev_langs:
- CSharp
helpviewer_keywords:
- Main method [C#]
- C# language, command-line arguments
- arguments [C#], command-line
- command line [C#], arguments
- command-line arguments [C#], Main method
ms.assetid: 73a17231-cf96-44ea-aa8a-54807c6fb1f4
caps.latest.revision: 30
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
ms.openlocfilehash: f6934a09c5f980f845e19b28e462cc601e154512
ms.lasthandoff: 03/13/2017

---
# <a name="main-and-command-line-arguments-c-programming-guide"></a>Main() e argomenti della riga di comando (Guida per programmatori C#)
Il metodo `Main` costituisce il punto di ingresso di un'applicazione console C# o di un'applicazione Windows. Le librerie e i servizi non richiedono un metodo `Main` come punto di ingresso. All'avvio dell'applicazione, `Main` è il primo metodo richiamato.  
  
 In un programma C# può essere presente un solo punto di ingresso. Se sono presenti più classi con un metodo `Main`, è necessario compilare il programma con l'opzione del compilatore **/main** per specificare quale metodo `Main` deve essere usato come punto di ingresso. Per altre informazioni, vedere [/main (Opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/main-compiler-option.md).  
  
 [!code-cs[csProgGuideMain#17](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-and-command-line-arguments_1.cs)]  
  
## <a name="overview"></a>Panoramica  
  
-   Il metodo `Main` è il punto di ingresso di un programma con estensione exe, ovvero il punto in cui il controllo del programma inizia e termina.  
  
-   `Main` viene dichiarato in una classe o in un tipo struct. `Main` deve essere impostato su [static](../../../csharp/language-reference/keywords/static.md) e non su [public](../../../csharp/language-reference/keywords/public.md). Nell'esempio precedente riceve l'accesso predefinito di [private](../../../csharp/language-reference/keywords/private.md). Non è necessario che la classe o il tipo struct che lo contiene sia statico.  
  
-   `Main` può avere un tipo restituito `void` o `int`.  
  
-   Il metodo `Main` può essere dichiarato con o senza un parametro `string[]` contenente argomenti della riga di comando. Quando si usa [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] per creare applicazioni Windows Form, è possibile aggiungere il parametro manualmente o usare la classe <xref:System.Environment> per ottenere gli argomenti della riga di comando. I parametri vengono letti come argomenti della riga di comando a indice zero. A differenza di quanto avviene in C e C++, il nome del programma non viene considerato il primo argomento della riga di comando.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)  
  
-   [Procedura: Visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)  
  
-   [Procedura: Accedere agli argomenti della riga di comando usando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)  
  
-   [Valori restituiti da Main()](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione dalla riga di comando con csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Contenuto di un programma C#](../../../csharp/programming-guide/inside-a-program/index.md)   
 [\<Applicazioni di esempio di C#](http://msdn.microsoft.com/en-us/9a9d7aaa-51d3-4224-b564-95409b0f3e15)
