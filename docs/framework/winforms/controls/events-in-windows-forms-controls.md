---
title: "Eventi nei controlli di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli personalizzati [Windows Form], cenni preliminari sugli eventi (mediante il codice)"
  - "eventi [Windows Form], controlli personalizzati (tramite codice)"
ms.assetid: 7e3d1379-87aa-437c-afce-c99454eff30e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Eventi nei controlli di Windows Form
Un controllo di Windows Form eredita più di sessanta eventi da <xref:System.Windows.Forms.Control?displayProperty=fullName>,  tra i quali l'evento <xref:System.Windows.Forms.Control.Paint>, responsabile del disegno del controllo, eventi correlati alla visualizzazione di finestre, quali <xref:System.Windows.Forms.Control.Resize> e <xref:System.Windows.Forms.Control.Layout>, nonché eventi della tastiera e del mouse di basso livello.  Alcuni eventi di basso livello sono sintetizzati da <xref:System.Windows.Forms.Control> in eventi semantici quali <xref:System.Windows.Forms.Control.Click> e <xref:System.Windows.Forms.Control.DoubleClick>.  Per ulteriori informazioni sugli eventi ereditati, vedere <xref:System.Windows.Forms.Control>.  
  
 Se è necessario che il controllo personalizzato sostituisca alcune funzionalità di eventi ereditati, eseguire l'override del metodo `On`*NomeEvento* anziché associare un delegato.  Se non si ha familiarità con il modello degli eventi di .NET Framework, vedere [Raising Events from a Component](../Topic/Raising%20Events%20from%20a%20Component.md).  
  
## Vedere anche  
 [Override del metodo OnPaint](../../../../docs/framework/winforms/controls/overriding-the-onpaint-method.md)   
 [Gestione dell'input dell'utente](../../../../docs/framework/winforms/controls/handling-user-input.md)   
 [Definizione di un evento](../../../../docs/framework/winforms/controls/defining-an-event-in-windows-forms-controls.md)   
 [Eventi](../../../../docs/standard/events/index.md)