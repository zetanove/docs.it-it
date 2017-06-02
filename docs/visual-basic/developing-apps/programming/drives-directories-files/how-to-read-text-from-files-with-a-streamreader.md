---
title: 'Procedura: Leggere il testo da file con un oggetto StreamReader (Visual Basic) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- reading files, text
- text, reading from files
- reading text from files
- files, reading
ms.assetid: 384033c6-18f9-4d59-9610-36371226558f
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: e53fe99a3b3292fc465271d667ef76053e61af51
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-read-text-from-files-with-a-streamreader-visual-basic"></a>Procedura: leggere il testo da file con un oggetto StreamReader (Visual Basic)
L'oggetto `My.Computer.FileSystem` offre metodi per aprire <xref:System.IO.TextReader> e <xref:System.IO.TextWriter>. `OpenTextFileWriter` e `OpenTextFileReader` sono metodi avanzati che non vengono visualizzati in IntelliSense, a meno che non venga selezionata la scheda **Tutti**.  
  
### <a name="to-read-a-line-from-a-file-with-a-text-reader"></a>Per leggere una riga da un file con il lettore di testo  
  
-   Usare il metodo `OpenTextFileReader` per aprire <xref:System.IO.TextReader>, specificando il file. In questo esempio viene aperto il file denominato `testfile.txt`, da cui una riga viene letta e visualizzata in una finestra di messaggio.  
  
     [!code-vb[VbFileIORead#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-text-from-files-with-a-streamreader_1.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Il file letto deve essere un file di testo.  
  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto. È possibile ad esempio che il file Form1.vb non sia un file di origine di Visual Basic.  
  
 Prima di usare i dati nell'applicazione verificare tutti gli input. È possibile che il contenuto del file non corrisponda a quanto previsto e che quindi i metodi per la lettura dal file non abbiano esito positivo.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Per leggere da un file, l'assembly richiede un livello di privilegi concesso dalla classe <xref:System.Security.Permissions.FileIOPermission>. Se eseguito in un contesto ad attendibilità parziale, il codice potrebbe generare un'eccezione a causa dell'insufficienza di privilegi. Per altre informazioni, vedere [Code Access Security Basics](https://msdn.microsoft.com/library/33tceax8) (Nozioni di base sulla sicurezza dell'accesso di codice). È anche necessario che l'utente possa accedere al file. Per altre informazioni, vedere [Panoramica della tecnologia ACL](http://msdn.microsoft.com/en-us/06fbf66d-6f02-4378-b863-b2f12e349045).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:System.Windows.Forms.OpenFileDialog>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A>   
 [SaveFileDialog Component](../../../../framework/winforms/controls/savefiledialog-component-windows-forms.md)   
 [Lettura da file](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)
