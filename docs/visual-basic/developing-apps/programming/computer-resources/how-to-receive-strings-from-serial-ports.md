---
title: 'Procedura: Ricevere stringhe da porte seriali in Visual Basic | Microsoft Docs'
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
- serial ports, retrieving strings
- strings [Visual Basic], retrieving from serial ports
- My.Resources object
ms.assetid: 8371ce2c-e1c7-476b-a86d-9afc2614b6b7
caps.latest.revision: 21
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
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: c535dcce1ad1b9a5fecd3c6a86d7fb522acf079e
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-receive-strings-from-serial-ports-in-visual-basic"></a>Procedura: ricevere stringhe da porte seriali in Visual Basic
Questo argomento descrive come usare `My.Computer.Ports` per ricevere stringhe dalle porte seriali del computer in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### <a name="to-receive-strings-from-the-serial-port"></a>Per ricevere stringhe dalla porta seriale  
  
1.  Inizializzare la stringa restituita.  
  
     [!code-vb[VbVbalrMyComputer#38](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_1.vb)]  
  
2.  Determinare quale porta seriale deve fornire le stringhe. In questo esempio si presuppone che sia `COM1`.  
  
3.  Usare il metodo `My.Computer.Ports.OpenSerialPort` per ottenere un riferimento alla porta. Per altre informazioni, vedere <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>.  
  
     Il blocco `Try...Catch...Finally` consente all'applicazione di chiudere la porta seriale anche se viene generata un'eccezione. Tutto il codice per la modifica della porta seriale deve essere contenuto all'interno di questo blocco.  
  
     [!code-vb[VbVbalrMyComputer#39](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_2.vb)]  
  
4.  Creare un ciclo `Do` per leggere le righe di testo fino a quando non sono più disponibili righe.  
  
     [!code-vb[VbVbalrMyComputer#40](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_3.vb)]  
  
5.  Usare il metodo <xref:System.IO.Ports.SerialPort.ReadLine%2A> per leggere la successiva riga di testo disponibile dalla porta seriale.  
  
     [!code-vb[VbVbalrMyComputer#41](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_4.vb)]  
  
6.  Usare un'istruzione `If` per determinare se il metodo <xref:System.IO.Ports.SerialPort.ReadLine%2A> restituisce `Nothing`, il che significa che non è più disponibile testo. Se restituisce `Nothing`, uscire dal ciclo `Do`.  
  
     [!code-vb[VbVbalrMyComputer#42](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_5.vb)]  
  
7.  Aggiungere un blocco `Else` all'istruzione `If` per gestire la situazione se la stringa viene effettivamente letta. Il blocco consente di aggiungere la stringa dalla porta seriale alla stringa restituita.  
  
     [!code-vb[VbVbalrMyComputer#43](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_6.vb)]  
  
8.  Restituire la stringa.  
  
     [!code-vb[VbVbalrMyComputer#44](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_7.vb)]  
  
## <a name="example"></a>Esempio  
 [!code-vb[VbVbalrMyComputer#37](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_8.vb)]  
  
 Questo esempio di codice è disponibile anche come frammento di codice IntelliSense. Nella selezione del frammento di codice si trova in **Connettività e rete**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Questo esempio presuppone l'uso della porta `COM1`.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Questo esempio presuppone l'uso della porta `COM1`. Per garantire una maggiore flessibilità, il codice deve consentire all'utente di selezionare la porta seriale desiderata da un elenco di porte disponibili. Per altre informazioni, vedere [Procedura: Mostrare le porte seriali disponibili](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md).  
  
 Questo esempio usa un blocco `Try...Catch...Finally` per verificare che l'applicazione chiuda la porta e per rilevare tutte le eccezioni di timeout. Per altre informazioni, vedere [Istruzione Try...Catch...Finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 <xref:System.IO.Ports.SerialPort?displayProperty=fullName>   
 [Procedura: Comporre numeri con modem collegati a porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-dial-modems-attached-to-serial-ports.md)   
 [Procedura: Inviare stringhe a porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [Procedura: Mostrare le porte seriali disponibili](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)
