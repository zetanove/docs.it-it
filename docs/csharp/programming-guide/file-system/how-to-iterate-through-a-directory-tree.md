---
title: 'Procedura: Eseguire l&quot;iterazione in un albero di directory (Guida per programmatori di C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- iterating through folders [C#]
- file iteration [C#]
ms.assetid: c4be4a75-6b1b-46a7-9d38-bab353091ed7
caps.latest.revision: 10
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
ms.openlocfilehash: c63e18bc7e23a9fda4a005745174bdd6c85b3f08
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-iterate-through-a-directory-tree-c-programming-guide"></a>Procedura: Scorrere un albero di directory (Guida per programmatori C#)
Eseguire l'iterazione in un albero di directory significa accedere a ogni file in ogni sottodirectory annidata in una cartella radice specificata, a qualsiasi livello. Non è necessario aprire ogni file. È possibile recuperare semplicemente il nome del file o della sottodirectory come `string`, oppure è possibile recuperare informazioni aggiuntive sotto forma di un oggetto <xref:System.IO.FileInfo?displayProperty=fullName> o <xref:System.IO.DirectoryInfo?displayProperty=fullName>.  
  
> [!NOTE]
>  In Windows i termini "directory" e "cartella" vengono usati indifferentemente. Nella maggior parte della documentazione e dell'interfaccia utente viene usato il termine "cartella", ma nella libreria di classi [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] viene usato il termine "directory".  
  
 Nel caso più semplice in cui si è certi di avere autorizzazioni di accesso per tutte le directory di una radice specificata, è possibile usare il flag `System.IO.SearchOption.AllDirectories`. Questo flag restituisce tutte le sottodirectory annidate che corrispondono al modello specificato. L'esempio seguente illustra come usare questo flag.  
  
```csharp  
root.GetDirectories("*.*", System.IO.SearchOption.AllDirectories);  
```  
  
 Il problema di questo approccio è che se una delle sottodirectory della radice specificata genera un'eccezione <xref:System.IO.DirectoryNotFoundException> o <xref:System.UnauthorizedAccessException>, l'intero metodo ha esito negativo e non restituisce alcuna directory. Lo stesso vale quando si usa il metodo <xref:System.IO.DirectoryInfo.GetFiles%2A>. Se è necessario gestire queste eccezioni in sottocartelle specifiche, procedere manualmente nell'albero di directory, come illustrato negli esempi seguenti.  
  
 Quando si procede manualmente in un albero di directory, è possibile gestire prima le sottodirectory (*attraversamento pre-ordine*), o prima i file (*attraversamento post-ordine*). Se si esegue un attraversamento pre-ordine, è necessario procedere lungo l'intero albero della cartella corrente prima di eseguire l'iterazione nei file direttamente in quella cartella. Gli esempi riportati più avanti nel documento eseguono l'attraversamento post-ordine ma è possibile modificarli per eseguire l'attraversamento pre-ordine.  
  
 Un'altra opzione consiste nell'usare la ricorsione o l'attraversamento basato su stack. Gli esempi più avanti in questo documento illustrano entrambi gli approcci.  
  
 Se è necessario eseguire una serie di operazioni su file e cartelle, è possibile modularizzare questi esempi effettuando il refactoring dell'operazione in funzioni separate che è possibile richiamare tramite un delegato unico.  
  
> [!NOTE]
>  I file system NTFS possono contenere *reparse point* sotto forma di *punti di giunzione*, *collegamenti simbolici* e *collegamenti reali*. I metodi di .NET Framework, come ad esempio <xref:System.IO.DirectoryInfo.GetFiles%2A> e <xref:System.IO.DirectoryInfo.GetDirectories%2A>, non restituiranno sottodirectory in un reparse point. Questo comportamento protegge dal rischio di entrare in un ciclo infinito quando due reparse point fanno riferimento uno all'altro. In generale, è necessario usare estrema cautela quando si usano i reparse point per evitare di modificare o eliminare file involontariamente. Se è necessario un controllo preciso dei reparse point, usare platform invoke o codice nativo per chiamare direttamente i metodi del file system Win32 appropriato.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come procedere in un albero di directory usando la ricursione. L'approccio ricorsivo è elegante ma può provocare un'eccezione di overflow dello stack se l'albero di directory è grande ed eccessivamente annidato.  
  
 Le eccezioni specifiche che vengono gestite e le azioni specifiche eseguite su ogni file o cartella vengono illustrate solo a titolo esemplificativo. Per soddisfare esigenze specifiche, è necessario modificare il codice. Per altre informazioni, vedere i commenti nel codice.  
  
 [!code-cs[csFilesandFolders#1](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-iterate-through-a-directory-tree_1.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come eseguire l'iterazione nei file e nelle cartelle in un albero di directory senza usare la ricorsione. Questa tecnica usa il tipo di raccolta generico <xref:System.Collections.Generic.Stack%601>, che è uno stack LIFO (Last in First out).  
  
 Le eccezioni specifiche che vengono gestite e le azioni specifiche eseguite su ogni file o cartella vengono illustrate solo a titolo esemplificativo. Per soddisfare esigenze specifiche, è necessario modificare il codice. Per altre informazioni, vedere i commenti nel codice.  
  
 [!code-cs[csFilesandFolders#2](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-iterate-through-a-directory-tree_2.cs)]  
  
 In genere testare ogni cartella per determinare se l'applicazione ha l'autorizzazione per aprirla richiede troppo tempo. Pertanto, l'esempio di codice racchiude quella parte dell'operazione in un blocco `try/catch`. È possibile modificare il blocco `catch` in modo che quando l'accesso a una cartella viene negato, si tenti di innalzare il livello delle autorizzazioni e quindi di accedere nuovamente. Come regola, rilevare solo le eccezioni che è possibile gestire senza lasciare l'applicazione in uno stato sconosciuto.  
  
 Se è necessario archiviare il contenuto di un albero di directory, in memoria o su disco, l'opzione migliore consiste nell'archiviare solo la proprietà <xref:System.IO.FileSystemInfo.FullName%2A>, di tipo `string`, per ogni file. È quindi possibile usare questa stringa per creare un nuovo oggetto <xref:System.IO.FileInfo> o <xref:System.IO.DirectoryInfo> in base alle esigenze o aprire i file che richiedono un'elaborazione ulteriore.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Un codice di iterazione file efficiente deve prendere in considerazione diversi aspetti complessi del file system. Per altre informazioni, vedere [NTFS Technical Reference](http://go.microsoft.com/fwlink/?LinkId=79488) (Riferimenti tecnici di NTFS).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO>   
 [Directory di file e LINQ (C#)](http://msdn.microsoft.com/library/5a5d516c-0279-4a84-ac84-b87f54caa808)   
 [File system e Registro di sistema (Guida per programmatori C#)](../../../csharp/programming-guide/file-system/index.md)
