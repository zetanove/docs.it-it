---
title: "Storing Data to and Reading from the Clipboard (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Clipboard, storing data to (My.Computer.Clipboard)"
  - "Clipboard, reading from (My.Computer.Clipboard)"
  - "Clipboard"
  - "My.Computer.Clipboard object, tasks"
  - "data [Visual Basic], Clipboard"
  - "reading data, from Clipboard"
ms.assetid: f690119a-4378-4f7d-b20e-d9377ef49496
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Storing Data to and Reading from the Clipboard (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile utilizzare gli Appunti per memorizzare dati, quali testo e immagini.  Poiché gli Appunti vengono condivisi da tutti i processi attivi, è possibile utilizzarli per trasferire i dati tra di essi.  L'oggetto di `My.Computer.Clipboard` consente di accedere facilmente agli Appunti e da leggere e scrivere.  
  
## Leggere dagli Appunti  
 Utilizzare il metodo di <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetText%2A> per leggere il testo negli Appunti.  Nel codice che segue il testo viene letto e visualizzato in una finestra di messaggio.  Per il corretto funzionamento dell'esempio, è necessario che negli Appunti sia memorizzato un testo.  
  
 [!code-vb[VbVbcnMyClipboard#4](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_1.vb)]  
  
 Questo esempio di codice è anche disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice si trova in **Sistema operativo Windows \> Appunti**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
 Utilizzare il metodo <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetImage%2A> per recuperare un'immagine dagli Appunti.  In questo esempio viene verificato se negli Appunti è presente un'immagine, prima di recuperarla e di assegnarla a  `PictureBox1`.  
  
 [!code-vb[VbResourceTasks#16](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_2.vb)]  
  
 Questo esempio di codice è anche disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice si trova in **Sistema operativo Windows \> Appunti**.Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
 Gli elementi inseriti negli Appunti saranno permanenti anche dopo la chiusura dell'applicazione.  
  
## Determinazione del tipo di file archiviato negli Appunti  
 I dati negli Appunti possono avere diverse forme, ad esempio testo, un file audio o un'immagine.  Per determinare quale tipo di file si trova negli Appunti, è possibile utilizzare metodi quali <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsAudio%2A>, <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsFileDropList%2A>, <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsImage%2A> e <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsText%2A>.  Se si desidera controllare un formato personalizzato, è possibile utilizzare il metodo <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsData%2A>.  
  
 Utilizzare la funzione `ContainsImage` per determinare se i dati contenuti negli Appunti sono un'immagine.  Il codice seguente controlla se i dati sono un'immagine e segnala il risultato della verifica.  
  
 [!code-vb[VbResourceTasks#13](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_3.vb)]  
  
## cancellare gli Appunti  
 Il metodo <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.Clear%2A> cancella gli Appunti.  Tale cancellazione può avere effetto sugli altri processi condivisi dagli Appunti.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare il metodo `Clear`.  
  
 [!code-vb[VbVbcnMyClipboard#3](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_4.vb)]  
  
## Scrivendo negli Appunti  
 Utilizzare il metodo <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetText%2A> per scrivere testo negli Appunti.  Il codice seguente scrive la stringa "This is a test string" negli Appunti.  
  
 [!code-vb[VbVbcnMyClipboard#1](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_5.vb)]  
  
 il metodo di `SetText` può accettare un parametro di formato che contiene un tipo di <xref:System.Windows.Forms.TextDataFormat>.  Il codice seguente scrive la stringa "This is a test string" negli Appunti come testo RTF.  
  
 [!code-vb[VbVbcnMyClipboard#2](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_6.vb)]  
  
 Utilizzare il metodo <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetData%2A> per scrivere i dati negli Appunti.  In questo esempio viene scritta la `dataChunk` dell'enumerazione `DataObject` negli Appunti nel formato personalizzato `specialFormat`.  
  
 [!code-vb[VbVbcnMyClipboard#7](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_7.vb)]  
  
 Utilizzare il metodo <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetAudio%2A> per scrivere i dati audio negli Appunti.  In questo esempio viene creata la matrice di byte `musicReader`, in cui viene letto il file `cool.wav`, che viene quindi scritto negli Appunti.  
  
 [!code-vb[VbResourceTasks#5](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/storing-data-to-and-read_8.vb)]  
  
> [!IMPORTANT]
>  Poiché il contenuto degli Appunti è accessibile da altri utenti, si consiglia di non utilizzarli per memorizzare informazioni riservate, ad esempio password o dati personali.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy>   
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetAudioStream%2A>   
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetDataObject%2A>   
 [Procedura: Leggere dati oggetto in un file XML](../Topic/How%20to:%20Read%20Object%20Data%20from%20an%20XML%20File%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: scrivere dati oggetto in un file XML](../Topic/How%20to:%20Write%20Object%20Data%20to%20an%20XML%20File%20\(C%23%20and%20Visual%20Basic\).md)