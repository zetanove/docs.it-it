---
title: 'Procedura: Scrivere in un file di testo (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- TextWriter.WriteLine
- StreamWriter.Close
dev_langs:
- CSharp
helpviewer_keywords:
- files [C#], text files
- text, writing to files [C#]
ms.assetid: 2e99f184-d88b-4719-a7f1-d9ec482aa809
caps.latest.revision: 23
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
ms.openlocfilehash: c56095582561e4df19b164bc9a46b69a14da7c9d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-write-to-a-text-file-c-programming-guide"></a>Procedura: scrivere in un file di testo (Guida per programmatori C#)
In questi esempi vengono mostrati vari modi per scrivere testo in un file.  I primi due esempi usano metodi pratici statici della classe <xref:System.IO.File?displayProperty=fullName> per scrivere ogni elemento di un oggetto IEnumerable\<string> e di una stringa in un file di testo.  Nell'esempio 3 viene illustrato come aggiungere testo a un file quando è necessario elaborare individualmente ogni riga mentre si scrive nel file.  Gli esempi da 1 a 3 sovrascrivono tutto il contenuto esistente nel file, ma l'esempio 4 mostra come aggiungere il testo a un file esistente.  
  
 In tutti gli esempi vengono scritti valori letterali stringa nei file, ma può essere più opportuno usare il metodo <xref:System.String.Format%2A>, che dispone di molti controlli per la scrittura di tipi diversi di valori giustificati a destra o a sinistra in un campo, con o senza riempimento e così via.  È anche possibile usare la funzionalità di [interpolazione di stringhe](../../../csharp/language-reference/keywords/interpolated-strings.md) di C#.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csFilesandFolders#3](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-write-to-a-text-file_1.cs)]  
  
 In tutti gli esempi vengono scritti valori letterali stringa nei file, ma può essere più opportuno usare il metodo <xref:System.String.Format%2A>, che dispone di molti controlli per la scrittura di tipi diversi di valori giustificati a destra o a sinistra in un campo, con o senza riempimento e così via.  È anche possibile usare la funzionalità di [interpolazione di stringhe](../../../csharp/language-reference/keywords/interpolated-strings.md) di C#.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il file esiste ed è di sola lettura.  
  
-   Il nome del percorso è troppo lungo.  
  
-   Il disco è pieno.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema (Guida per programmatori C#)](../../../csharp/programming-guide/file-system/index.md)   
 [Come salvare una raccolta di oggetti personalizzati nella memoria locale](http://code.msdn.microsoft.com/CSWinStoreAppSaveCollection-bed5d6e6)
