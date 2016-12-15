---
title: "How to: Receive Strings From Serial Ports in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "serial ports, retrieving strings"
  - "strings [Visual Basic], retrieving from serial ports"
  - "My.Resources object"
ms.assetid: 8371ce2c-e1c7-476b-a86d-9afc2614b6b7
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Receive Strings From Serial Ports in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento viene descritto come utilizzare `My.Computer.Ports` per ricevere stringhe dalle porte seriali del computer in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### Per ricevere stringhe dalla porta seriale  
  
1.  Inizializzare la stringa restituita.  
  
     [!code-vb[VbVbalrMyComputer#38](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_1.vb)]  
  
2.  Determinare quale porta seriale deve fornire le stringhe.  In questo esempio si presuppone che sia `COM1`.  
  
3.  Utilizzare il metodo `My.Computer.Ports.OpenSerialPort` per ottenere un riferimento alla porta.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>.  
  
     Il blocco `Try...Catch...Finally` consente all'applicazione di chiudere la porta seriale anche se viene generata un'eccezione.  Tutto il codice per la modifica della porta seriale deve essere contenuto all'interno di questo blocco.  
  
     [!code-vb[VbVbalrMyComputer#39](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_2.vb)]  
  
4.  Creare un ciclo `Do` per leggere le righe di testo fino a quando non sono più disponibili righe.  
  
     [!code-vb[VbVbalrMyComputer#40](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_3.vb)]  
  
5.  Utilizzare il metodo <xref:System.IO.Ports.SerialPort.ReadLine%2A> per leggere la successiva riga di testo disponibile dalla porta seriale.  
  
     [!code-vb[VbVbalrMyComputer#41](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_4.vb)]  
  
6.  Utilizzare un'istruzione `If` per determinare se il metodo <xref:System.IO.Ports.SerialPort.ReadLine%2A> restituisce `Nothing`, il che significa che non è più disponibile testo.  Se restituisce `Nothing`, uscire dal ciclo `Do`.  
  
     [!code-vb[VbVbalrMyComputer#42](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_5.vb)]  
  
7.  Aggiungere un blocco `Else` all'istruzione `If` per gestire la situazione se la stringa viene effettivamente letta.  Il blocco consente di aggiungere la stringa dalla porta seriale alla stringa restituita.  
  
     [!code-vb[VbVbalrMyComputer#43](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_6.vb)]  
  
8.  Restituire la stringa.  
  
     [!code-vb[VbVbalrMyComputer#44](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_7.vb)]  
  
## Esempio  
 [!code-vb[VbVbalrMyComputer#37](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-receive-strings-from-serial-ports_8.vb)]  
  
 Questo esempio di codice è anche disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice, si trova in **Connettività e rete**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
## Compilazione del codice  
 In questo esempio si presuppone che venga utilizzata la porta `COM1`.  
  
## Programmazione efficiente  
 In questo esempio si presuppone che venga utilizzata la porta `COM1`.  Per garantire una maggiore flessibilità, il codice deve consentire all'utente di selezionare la porta seriale desiderata da un elenco di porte disponibili.  Per ulteriori informazioni, vedere [How to: Show Available Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md).  
  
 In questo esempio viene utilizzato un blocco `Try...Catch...Finally` per verificare che l'applicazione chiuda la porta e per rilevare tutte le eccezioni di timeout.  Per ulteriori informazioni, vedere [Try...Catch...Finally Statement](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 <xref:System.IO.Ports.SerialPort?displayProperty=fullName>   
 [How to: Dial Modems Attached to Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-dial-modems-attached-to-serial-ports.md)   
 [How to: Send Strings to Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [How to: Show Available Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)