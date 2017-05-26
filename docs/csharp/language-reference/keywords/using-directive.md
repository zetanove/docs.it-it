---
title: Direttiva using (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- using directive [C#]
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
caps.latest.revision: 31
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e91cc4fea9fbe57b257e17915cd28b3b82f12f6e
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="using-directive-c-reference"></a>Direttiva using (Riferimenti per C#)
La direttiva `using` ha tre usi:  
  
-   Consentire l'uso di tipi in uno spazio dei nomi in modo da non dover qualificare l'uso di un tipo in tale spazio dei nomi:  
  
    ```csharp  
    using System.Text;  
    ```  
  
-   Consentire l'accesso ai membri statici di un tipo senza dover qualificare l'accesso con il nome del tipo. 
  
    ```csharp  
    using static System.Math;  
    ```  
     
    Per altre informazioni, vedere la [direttiva using static](using-static.md).

-   Creare un alias per uno spazio dei nomi o un tipo. Si tratta di una *direttiva alias using*.  
  
    ```csharp  
    using Project = PC.MyCompany.Project;  
    ```  
  
 La parola chiave `using` viene usata anche per creare *istruzioni using*, che garantiscono la gestione corretta degli oggetti <xref:System.IDisposable>. Per altre informazioni, vedere [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md).  
  
## <a name="using-static-type"></a>Tipo using static  
 È possibile accedere ai membri statici di un tipo senza dover qualificare l'accesso con il nome del tipo:  
  
```csharp  
using static System.Console;   
using static System.Math;  
class Program   
{   
    static void Main()   
    {   
        WriteLine(Sqrt(3*3 + 4*4));   
    }   
}  
```  
  
## <a name="remarks"></a>Note  
 L'ambito di una direttiva `using` è limitato al file in cui viene visualizzata.  
  
 Creare un alias `using` per semplificare la qualifica di un identificatore in uno spazio dei nomi o un tipo. La parte destra di una direttiva alias deve essere sempre un tipo completo indipendentemente dalle direttive using che lo precedono.  
  
 Creare una direttiva `using` per usare i tipi in uno spazio dei nomi senza dover specificare tale spazio dei nomi. Una direttiva `using` non offre accesso ad alcuno spazio dei nomi annidato nello spazio dei nomi specificato.  
  
 Gli spazi dei nomi sono disponibili in due categorie: definiti dall'utente e definiti dal sistema. Gli spazi dei nomi definiti dall'utente vengono definiti nel codice. Per un elenco di spazi dei nomi definiti dal sistema, vedere [Libreria di classi di .NET Framework](http://go.microsoft.com/fwlink/?LinkID=227195).  
  
 Per esempi relativi ai metodi di riferimento in altri assembly, vedere [Creazione e uso di DLL C#](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4).  
  
## <a name="example-1"></a>Esempio 1  
  
 Nell'esempio seguente viene illustrato come definire e usare un alias `using` per uno spazio dei nomi.  
  
 [!code-cs[csrefKeywordsNamespace#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_1.cs)]  
  
 Una direttiva alias using non può contenere un tipo generico aperto nella parte destra. Ad esempio, non è possibile creare un alias using per List\<T>, ma è possibile crearne uno per List\<int>.  
  
## <a name="example-2"></a>Esempio 2  
  
 Nell'esempio seguente viene illustrato come definire una direttiva `using` e un alias `using` per una classe:  
  
 [!code-cs[csrefKeywordsNamespace#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_2.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Uso degli spazi dei nomi](../../../csharp/programming-guide/namespaces/using-namespaces.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per gli spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)   
 [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md)

