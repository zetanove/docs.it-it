---
title: 'Procedura: Leggere un file di testo una riga alla volta (Visual C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- ReadLine method [C#]
- reading text files, line by line
- text files [C#]
ms.assetid: d62e22c5-a13c-48db-af9b-f10c801b0cb1
caps.latest.revision: 11
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
ms.openlocfilehash: 957022bd4c6244321361e39cfbdf52cf4071e2d8
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-a-text-file-one-line-at-a-time-visual-c"></a>Procedura: leggere un file di testo una riga alla volta (Visual C#)
Questo esempio legge il contenuto di un file di testo, una riga alla volta, in una stringa usando il metodo `ReadLine` della classe `StreamReader`. Ogni riga di testo è memorizzata nella stringa `line` e visualizzata nella schermata.  
  
## <a name="example"></a>Esempio  
  
```  
int counter = 0;  
string line;  
  
// Read the file and display it line by line.  
System.IO.StreamReader file =   
    new System.IO.StreamReader(@"c:\test.txt");  
while((line = file.ReadLine()) != null)  
{  
    System.Console.WriteLine (line);  
    counter++;  
}  
  
file.Close();  
System.Console.WriteLine("There were {0} lines.", counter);  
// Suspend the screen.  
System.Console.ReadLine();  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Copiare il codice e incollarlo nel metodo `Main` di un'applicazione console.  
  
 Sostituire `"c:\test.txt"` con il nome effettivo del file.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   È possibile che il file non esista.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto. Ad esempio, il file `myFile.cs` potrebbe non essere un file di origine C#.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema (Guida per programmatori C#)](../../../csharp/programming-guide/file-system/index.md)
