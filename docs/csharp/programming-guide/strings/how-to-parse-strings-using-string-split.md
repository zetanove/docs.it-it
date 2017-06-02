---
title: 'Procedura: Analizzare le stringhe con String.Split (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- splitting strings [C#]
- Split method [C#]
- strings [C#], splitting
- parse strings
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 1f5f15c305619c538aa276396c31296f42c8f40a
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="how-to-parse-strings-using-stringsplit-c-programming-guide"></a>Procedura: Analizzare le stringhe con String.Split (Guida per programmatori C#)
L'esempio di codice seguente illustra come analizzare una stringa con il metodo <xref:System.String.Split%2A?displayProperty=fullName>. <xref:System.String.Split%2A> accetta come input una matrice di caratteri che indica quali caratteri separano le sottostringhe rilevanti della stringa di destinazione.  La funzione restituisce una matrice di sottostringhe.  
  
 Questo esempio usa spazi, virgole, punti, due punti e tabulazioni, tutti passati in una matrice che contiene questi caratteri di separazione per <xref:System.String.Split%2A>.  Ogni parola nella frase della stringa di destinazione viene visualizzata separatamente rispetto alla matrice di stringhe risultante.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideStrings#16](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-parse-strings-using-string-split_1.cs)]  
  
## <a name="example"></a>Esempio  
 Per impostazione predefinita, String.Split restituisce stringhe vuote quando vengono visualizzati due caratteri di separazione adiacenti nella stringa di destinazione.  È possibile passare un parametro facoltativo StringSplitOptions.RemoveEmptyEntries per escludere le stringhe vuote nell'output.  
  
 String.Split può accettare una matrice di stringhe (sequenze di caratteri, al posto di caratteri singoli, che fungono da separatori per l'analisi della stringa di destinazione).  
  
```csharp  
class TestStringSplit  
{  
    static void Main()  
    {  
        char[] separatingChars = { "<<", "..." };  
  
        string text = "one<<two......three<four";  
        System.Console.WriteLine("Original text: '{0}'", text);  
  
        string[] words = text.Split(separatingChars, System.StringSplitOptions.RemoveEmptyEntries );  
        System.Console.WriteLine("{0} substrings in text:", words.Length);  
  
        foreach (string s in words)  
        {  
            System.Console.WriteLine(s);  
        }  
  
        // Keep the console window open in debug mode.  
        System.Console.WriteLine("Press any key to exit.");  
        System.Console.ReadKey();  
    }  
}  
/* Output:  
    Original text: 'one<<two......three<four'  
    3 words in text:  
    one  
    two  
    three<four  
*/  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [Espressioni regolari di .NET Framework](https://msdn.microsoft.com/library/hs600312)

