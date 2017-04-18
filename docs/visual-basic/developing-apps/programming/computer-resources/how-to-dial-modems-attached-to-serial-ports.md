---
title: 'Procedura: Comporre numeri con modem collegati a porte seriali in Visual Basic | Documentazione Microsoft'
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
- modems, dialing
- serial ports, dialing
- My.Computer.Ports object
ms.assetid: 3834db40-f431-45f1-b671-dc91787164b6
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4916c7bc3fc60b25dba8386294f11d07346cb358
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-dial-modems-attached-to-serial-ports-in-visual-basic"></a>Procedura: comporre numeri con modem collegati a porte seriali in Visual Basic
In questo argomento viene descritto come usare `My.Computer.Ports` per comporre numeri con modem in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 In genere, il modem è collegato a una delle porte seriali del computer. Affinché l'applicazione comunichi con il modem, è necessario inviare i comandi alla porta seriale appropriata.  
  
### <a name="to-dial-a-modem"></a>Comporre numeri con modem  
  
1.  Determinare a quale porta seriale è connesso il modem. Nell'esempio si presuppone che il modem sia collegato a COM1.  
  
2.  Usare il metodo `My.Computer.Ports.OpenSerialPort` per ottenere un riferimento alla porta. Per altre informazioni, vedere <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>.  
  
     Il blocco `Using` consente all'applicazione di chiudere la porta seriale, anche se viene generata un'eccezione. Tutto il codice relativo alla porta seriale deve essere all'interno di questo blocco o di un blocco `Try...Catch...Finally`.  
  
     [!code-vb[VbVbalrMyComputer#28](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-dial-modems-attached-to-serial-ports_1.vb)]  
  
3.  Impostare la proprietà `DtrEnable` per indicare che il computer è pronto ad accettare una trasmissione in ingresso dal modem.  
  
     [!code-vb[VbVbalrMyComputer#29](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-dial-modems-attached-to-serial-ports_2.vb)]  
  
4.  Inviare il comando di connessione e il numero di telefono al modem attraverso la porta seriale usando il metodo <xref:System.IO.Ports.SerialPort.Write%2A>.  
  
     [!code-vb[VbVbalrMyComputer#30](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-dial-modems-attached-to-serial-ports_3.vb)]  
  
## <a name="example"></a>Esempio  
 [!code-vb[VbVbalrMyComputer#27](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-dial-modems-attached-to-serial-ports_4.vb)]  
  
 Questo esempio di codice è disponibile anche come frammento di codice IntelliSense. Nella selezione del frammento di codice, si trova in **Connettività e rete**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Per questo esempio è necessario un riferimento allo spazio dei nomi <xref:System?displayProperty=fullName>.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Nell'esempio si presuppone che il modem sia collegato a COM1. È consigliabile che il codice consenta all'utente di selezionare la porta seriale desiderata da un elenco di porte disponibili. Per altre informazioni, vedere [Procedura: Mostrare le porte seriali disponibili](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md).  
  
 Questo esempio usa un blocco `Using` per verificare che l'applicazione chiuda la porta anche se viene generata un'eccezione. Per altre informazioni, vedere [Istruzione using](../../../../visual-basic/language-reference/statements/using-statement.md).  
  
 In questo esempio, l'applicazione si disconnette dalla porta seriale dopo aver composto il numero con il modem. In uno scenario reale, l'utente vuole trasferire i dati da e verso il modem. Per altre informazioni, vedere [Procedura: Ricevere stringhe da porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 <xref:System.IO.Ports.SerialPort?displayProperty=fullName>   
 [Procedura: Inviare stringhe a porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [Procedura: Ricevere stringhe da porte seriali](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)   
 [Procedura: Mostrare le porte seriali disponibili](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)
