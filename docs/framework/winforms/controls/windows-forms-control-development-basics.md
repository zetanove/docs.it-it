---
title: "Nozioni fondamentali sullo sviluppo di controlli Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], creazione"
  - "controlli personalizzati [Windows Form], tipi derivati"
  - "concetti di programmazione, controlli Windows Form"
ms.assetid: 6277bb81-90f7-4c5b-9f4b-b02bb42dd316
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Nozioni fondamentali sullo sviluppo di controlli Windows Form
Un controllo di Windows Form è una classe derivata direttamente o indirettamente da <xref:System.Windows.Forms.Control?displayProperty=fullName>.  Nell'elenco che segue sono descritti scenari comuni per lo sviluppo di controlli Windows Form.  
  
-   Combinazione di controlli esistenti in modo da creare un controllo composito.  
  
     I controlli compositi incapsulano un'interfaccia utente riutilizzabile come controllo.  Un esempio di controllo composito è un controllo costituito da una casella di testo e da un pulsante Reimposta.  Le finestre di progettazione visive offrono un ricco supporto per la creazione di controlli compositi.  Per modificare un controllo composito è necessario derivarlo da <xref:System.Windows.Forms.UserControl?displayProperty=fullName>.  La classe base <xref:System.Windows.Forms.UserControl> fornisce il routing da tastiera per i controlli figlio e consente il funzionamento di tali controlli come gruppo.  Per ulteriori informazioni, vedere [Sviluppo di un controllo Windows Form composto](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md).  
  
-   Estensione di un controllo esistente per personalizzarlo o associarvi funzionalità aggiuntive.  
  
     Sono esempi di controlli estesi un pulsante di cui non è possibile modificare il colore e un pulsante che presenta una proprietà aggiuntiva che registra il numero di volte in cui viene fatto clic sul pulsante stesso.  È possibile personalizzare qualsiasi controllo Windows Form derivando un altro controllo da esso, quindi eseguendo l'override o l'aggiunta di proprietà, metodi ed eventi.  
  
-   Creazione di un controllo che non combina o estende controlli esistenti.  
  
     In questo scenario occorre derivare il controllo dalla classe base <xref:System.Windows.Forms.Control>.  È possibile sia eseguire l'override di proprietà, metodi ed eventi della classe base sia aggiungerne di nuovi.  Per un'introduzione, vedere [Procedura: sviluppare un controllo di Windows Form semplice](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md).  
  
 La classe base per i controlli di Windows Forms <xref:System.Windows.Forms.Control> fornisce l'infrastruttura necessaria per la visualizzazione nelle applicazioni basate su Windows sul lato client.  <xref:System.Windows.Forms.Control> rende disponibile un handle di finestra, gestisce il routing dei messaggi e fornisce eventi del mouse e della tastiera oltre a numerosi altri eventi dell'interfaccia utente.  Inoltre offre un layout avanzato e presenta proprietà specifiche per la visualizzazione, quali <xref:System.Windows.Forms.Control.ForeColor%2A>, <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.Height%2A>,<xref:System.Windows.Forms.Control.Width%2A> e molte altre.  Fornisce infine funzionalità di sicurezza, supporto del threading e interoperabilità con controlli ActiveX.  Dal momento che una parte così consistente dell'infrastruttura è fornita dalla classe base, è relativamente semplice sviluppare controlli Windows Form personalizzati.  
  
## Vedere anche  
 [Procedura: sviluppare un controllo di Windows Form semplice](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)   
 [Sviluppo di un controllo Windows Form composto](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md)   
 [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)   
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)