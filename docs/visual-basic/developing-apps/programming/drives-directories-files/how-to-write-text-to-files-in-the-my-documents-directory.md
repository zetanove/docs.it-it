---
title: 'Procedura: Scrivere testo in file della directory Documenti in Visual Basic| Microsoft Docs'
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
- files, writing to
- text, writing to files
- examples [Visual Basic], text files
- writing to files, in My Documents
ms.assetid: 1c726124-781d-4976-9baa-ed46814ff3fe
caps.latest.revision: 19
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
ms.openlocfilehash: 848f7c3eac56f85d2af4c613645d54b70061d072
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-write-text-to-files-in-the-my-documents-directory-in-visual-basic"></a>Procedura: scrivere testo in file della directory Documenti in Visual Basic
L'oggetto `My.Computer.FileSystem.SpecialDirectories` consente di accedere a directory speciali, ad esempio alla directory **Documenti**.  
  
## <a name="procedure"></a>Procedura  
  
#### <a name="to-write-new-text-files-in-the-my-documents-directory"></a>Per scrivere nuovo testo nei file della directory Documenti  
  
1.  Usare la proprietà `My.Computer.FileSystem.SpecialDirectories.MyDocuments` per specificare il percorso.  
  
     [!code-vb[VbFileIOWrite#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_1.vb)]  
  
2.  Usare il metodo `WriteAllText` per scrivere testo nel file indicato.  
  
     [!code-vb[VbVbcnMyFileSystem#14](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_2.vb)]  
  
## <a name="example"></a>Esempio  
 [!code-vb[VbFileIOWrite#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_3.vb)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Sostituire `test.txt` con il nome del file in cui si vuole scrivere.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 In questo codice vengono rigenerate tutte le eccezioni che possono verificarsi durante la scrittura di testo nel file. È possibile ridurre la probabilità di eccezioni usando i controlli Windows Form, ad esempio i controlli dei componenti [OpenFileDialog](../../../../framework/winforms/controls/openfiledialog-component-windows-forms.md) e [SaveFileDialog](../../../../framework/winforms/controls/savefiledialog-component-windows-forms.md) che limitano le scelte dell'utente a nomi di file validi. L'uso di questi controlli non è comunque infallibile. Il file system può subire variazioni nel tempo che intercorre tra la selezione di un file da parte dell'utente e il momento in cui il codice viene eseguito. Quando si usano i file, è quindi quasi sempre necessaria la gestione delle eccezioni.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Se eseguito in un contesto ad attendibilità parziale, il codice potrebbe generare un'eccezione a causa dell'insufficienza di privilegi. Per altre informazioni, vedere [Code Access Security Basics](https://msdn.microsoft.com/library/33tceax8) (Nozioni di base sulla sicurezza dell'accesso di codice).  
  
 In questo esempio viene creato un nuovo file. Per poter creare un file in un'applicazione, è necessario che l'applicazione disponga dell'autorizzazione per la creazione della cartella. Le autorizzazioni vengono impostate tramite gli elenchi di controllo di accesso. Se il file è già esistente, l'applicazione necessita solo dell'autorizzazione di scrittura, ossia di un privilegio di livello inferiore. Laddove possibile, è più sicuro creare il file durante la fase di distribuzione e concedere privilegi di lettura a un unico file, anziché concedere privilegi per la creazione di una cartella. È anche più sicuro scrivere i dati nelle cartelle utente anziché nella cartella radice o nella cartella **Programmi**. Per altre informazioni, vedere [Panoramica della tecnologia ACL](http://msdn.microsoft.com/en-us/06fbf66d-6f02-4378-b863-b2f12e349045).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO.Path.Combine%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>   
 <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>
