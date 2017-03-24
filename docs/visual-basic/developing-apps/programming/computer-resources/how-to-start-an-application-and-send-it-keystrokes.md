---
title: "How to: Start an Application and Send it Keystrokes (Visual Basic) | Microsoft Docs"
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
  - "keystrokes, sending"
  - "Shell command example [Visual Basic]"
  - "processes, starting and sending keystrokes"
  - "SendKeys.SendWait examples"
ms.assetid: f1303184-fce4-44fb-88b4-aac5f42d5d77
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Start an Application and Send it Keystrokes (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo esempio viene utilizzata la funzione `Shell` per avviare la calcolatrice e quindi vengono moltiplicati due numeri mediante l'invio di sequenze di tasti con il metodo `My.Computer.Keyboard.SendKeys`.  
  
## Esempio  
 [!code-vb[VbVbalrMyComputer#25](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-start-an-application-and-send-it-keystrokes_1.vb)]  
  
## Programmazione efficiente  
 Se non viene rilevata alcuna applicazione con l'identificatore di processo richiesto viene generata l'eccezione <xref:System.ArgumentException>.  
  
## Sicurezza di .NET Framework  
 La chiamata alla funzione `Shell` richiede attendibilità totale \(classe <xref:System.Security.SecurityException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Keyboard.SendKeys%2A>   
 <xref:Microsoft.VisualBasic.Interaction.Shell%2A>   
 <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>