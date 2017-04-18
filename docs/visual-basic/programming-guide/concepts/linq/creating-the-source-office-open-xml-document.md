---
title: Creazione del documento di origine Office Open XML (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 61ccd6fb-0c47-4075-afdf-5b5021330f21
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 928a3c34836464e7603c485b64c9c426913ae7b2
ms.lasthandoff: 03/13/2017


---
# <a name="creating-the-source-office-open-xml-document-visual-basic"></a>Creazione del documento di origine Office Open XML (Visual Basic)
In questo argomento viene illustrato come creare il documento WordprocessingML di Office Open XML usato in altri esempi di questa esercitazione. Seguendo queste istruzioni, l'output ottenuto sarà uguale a quello indicato in ogni esempio.  
  
 Tuttavia, gli esempi presentati in questa esercitazione funzioneranno con qualsiasi documento WordprocessingML valido.  
  
 Per creare il documento usato in questa esercitazione, è necessario selezionare Microsoft Office 2007 o versione successiva oppure è necessario Microsoft Office 2003 con Microsoft Office Compatibility Pack per Word, Excel e formati di File di PowerPoint 2007.  
  
## <a name="creating-the-wordprocessingml-document"></a>Creazione del documento WordprocessingML  
  
#### <a name="to-create-the-wordprocessingml-document"></a>Per creare il documento WordprocessingML  
  
1.  Creare un nuovo documento di Microsoft Word.  
  
2.  Incollare il testo seguente nel nuovo documento:  
  
    ```  
    Parsing WordprocessingML with LINQ to XML  
  
    The following example prints to the console.  
  
    Imports System  
  
    Class Program  
        Public Shared  Sub Main(ByVal args() As String)  
            Console.WriteLine("Hello World")  
        End Sub  
    End Class  
  
    This example produces the following output:  
  
    Hello World  
    ```  
  
3.  Formattare la prima riga con lo stile "Intestazione 1".  
  
4.  Selezionare le righe che contengono il codice Visual Basic. La prima riga inizia con la parola chiave `Imports`. L'ultima riga è "End Class". Formattare le righe con il tipo di carattere Courier. Formattarle con un nuovo stile, da denominare "Code".  
  
5.  Infine, selezionare l'intera riga che contiene l'output e formattarla con lo stile `Code`.  
  
6.  Salvare il documento e denominarlo SampleDoc.docx.  
  
    > [!NOTE]
    >  Se si utilizza Microsoft Word 2003, selezionare **documento di Word 2007** nel **Salva come tipo** elenco a discesa.  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione: Manipolazione di contenuto in un documento WordprocessingML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
