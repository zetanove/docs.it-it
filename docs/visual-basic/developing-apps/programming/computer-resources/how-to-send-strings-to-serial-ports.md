---
title: "How to: Send Strings to Serial Ports in Visual Basic | Microsoft Docs"
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
  - "ports, sending strings to"
  - "strings [Visual Basic], sending to serial ports"
  - "My.Computer.Ports object"
  - "serial ports, sending strings to"
ms.assetid: 6ebf46cd-b2d0-4b2c-9a1f-be177b22ad52
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Send Strings to Serial Ports in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento viene descritto come utilizzare `My.Computer.Ports` per inviare stringhe alle porte seriali del computer in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## Esempio  
 In questo esempio viene inviata una stringa alla porta seriale COM1.  Potrebbe essere necessario utilizzare una porta seriale diversa del computer.  
  
 Utilizzare il metodo `My.Computer.Ports.OpenSerialPort` per ottenere un riferimento alla porta.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>.  
  
 Il blocco `Using` consente all'applicazione di chiudere la porta seriale anche se viene generata un'eccezione.  Tutto il codice per la modifica della porta seriale deve essere contenuto all'interno di questo blocco o di un blocco `Try...Catch...Finally`.  
  
 Il metodo <xref:System.IO.Ports.SerialPort.WriteLine%2A> invia i dati alla porta seriale.  
  
 [!code-vb[VbVbalrMyComputer#33](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-send-strings-to-serial-ports_1.vb)]  
  
## Compilazione del codice  
  
-   In questo esempio si presuppone che venga utilizzata la porta `COM1`.  
  
## Programmazione efficiente  
 Nell'esempio si suppone che il computer utilizzi la porta `COM1`; per maggiore flessibilità, il codice dovrebbe consentire all'utente di selezionare la porta seriale desiderata da un elenco di porte disponibili.  Per ulteriori informazioni, vedere [How to: Show Available Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md).  
  
 Nell'esempio riportato di seguito viene utilizzato un blocco `Using` per accertarsi che l'applicazione chiuda la porta anche se genera un'eccezione.  Per ulteriori informazioni, vedere [Using Statement](../../../../visual-basic/language-reference/statements/using-statement.md).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 <xref:System.IO.Ports.SerialPort?displayProperty=fullName>   
 [How to: Dial Modems Attached to Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-dial-modems-attached-to-serial-ports.md)   
 [How to: Show Available Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)