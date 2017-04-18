---
title: 'Procedura: Mostrare le porte seriali disponibili in Visual Basic | Microsoft Docs'
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
- serial ports, availability
- My.Computer.Ports.SerialPortNames property
- My.Computer.Ports object
- ports, serial port availability
ms.assetid: eaf2ee5a-8103-4e10-a205-ed1d4db120ba
caps.latest.revision: 20
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cc316600acd5f551dad8fbd4b7260c512231da5e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-show-available-serial-ports-in-visual-basic"></a>Procedura: mostrare le porte seriali disponibili in Visual Basic
Questo argomento descrive come usare `My.Computer.Ports` per visualizzare in Visual Basic le porte seriali disponibili del computer[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Per consentire agli utenti di selezionare la porta da usare, i nomi delle porte seriali si trovano in un controllo <xref:System.Windows.Forms.ListBox>.  
  
## <a name="example"></a>Esempio  
 Questo esempio esegue il ciclo attraverso tutte le stringhe restituite dalla proprietà `My.Computer.Ports.SerialPortNames`. Queste stringhe rappresentano i nomi delle porte seriali disponibili nel computer.  
  
 In genere, gli utenti selezionano la porta seriale che l'applicazione deve usare dall'elenco delle porte disponibili. In questo esempio i nomi delle porte seriali sono archiviati in un controllo <xref:System.Windows.Forms.ListBox>. Per altre informazioni, vedere [Controllo ListBox](http://msdn.microsoft.com/library/b0172473-c5f2-411e-aaa4-c8f17cb5eed4).  
  
 [!code-vb[VbVbalrMyComputer#45](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-show-available-serial-ports_1.vb)]  
  
 Questo esempio di codice è disponibile anche come frammento di codice IntelliSense. All'interno della casella di selezione dei frammenti di codice si trova in **Connettività e rete**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un riferimento del progetto a System.Windows.Forms.dll.  
  
-   Accesso ai membri dello spazio dei nomi <xref:System.Windows.Forms>. Aggiungere un'istruzione `Imports` se i nomi dei membri all'interno del codice non sono specificati in modo completo. Per altre informazioni, vedere [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
-   Presenza all'interno del form di un controllo <xref:System.Windows.Forms.ListBox> denominato `ListBox1`.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Non è necessario usare il controllo <xref:System.Windows.Forms.ListBox> per visualizzare i nomi delle porte seriali disponibili. In alternativa, è possibile usare un controllo <xref:System.Windows.Forms.ComboBox> o un altro controllo. Se l'applicazione non richiede una risposta da parte dell'utente, è possibile usare un controllo <xref:System.Windows.Forms.TextBox> per visualizzare le informazioni.  
  
> [!NOTE]
>  I nomi delle porte restituiti da `My.Computer.Ports.SerialPortNames` potrebbero non essere corretti se l'applicazione viene eseguita con Windows 98. Per evitare errori dell'applicazione, usare la funzione di gestione delle eccezioni, ad esempio l'istruzione `Try...Catch...Finally` o `Using`, quando per aprire le porte si usano i nomi delle porte stesse.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 [Procedura: Comporre numeri con modem collegati a porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-dial-modems-attached-to-serial-ports.md)   
 [Procedura: Inviare stringhe a porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [Procedura: Ricevere stringhe da porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)
