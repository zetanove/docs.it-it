---
title: "Mouse Capture in Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "mouse, capture"
ms.assetid: 8911d4b0-a4f8-4f93-8246-371aebd27d0c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Mouse Capture in Windows Forms
Per *mouse capture* si intende l'assunzione del comando dell'input completo del mouse da parte di un controllo.  Quando un controllo detiene il mouse capture, riceve l'input del mouse anche se il puntatore non rientra nei suoi limiti.  
  
## Impostazione di mouse capture  
 In Windows Form il mouse capture viene acquisito da un controllo quando l'utente preme un pulsante del mouse sul controllo e viene rilasciato dal controllo quando l'utente rilascia il pulsante del mouse.  
  
 La proprietà <xref:System.Windows.Forms.Control.Capture%2A> della classe <xref:System.Windows.Forms.Control> specifica se un controllo detiene il mouse capture.  Per determinare il momento in cui un controllo perde il mouse capture, gestire l'evento <xref:System.Windows.Forms.Control.MouseCaptureChanged>.  
  
 Solo la finestra in primo piano può ricevere l'input del mouse.  Quando una finestra in background tenta di acquisire il mouse capture, riceve messaggi solo per gli eventi del mouse che si verificano quando il puntatore rientra nella parte visibile della finestra.  Anche quando il mouse capture avviene nella finestra in primo piano, inoltre, è sempre possibile fare clic su un'altra finestra per portarla in primo piano.  Quando avviene il mouse capture, i tasti di scelta rapida non sono attivi.  
  
## Vedere anche  
 [Mouse Input in a Windows Forms Application](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)