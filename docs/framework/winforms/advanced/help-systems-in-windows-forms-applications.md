---
title: "Help Systems in Windows Forms Applications | Microsoft Docs"
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
  - "Help, adding to Windows applications"
  - "Windows applications, providing Help systems"
  - "What's This? Help"
  - "Help, Windows Forms"
  - "HelpProvider component [Windows Forms], providing Help in Windows applications"
ms.assetid: 2a96a278-432c-41fc-9e3c-5bfedf5e1267
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Help Systems in Windows Forms Applications
Un valido sistema di Guida è sicuramente una funzionalità molto utile per gli utenti,  in quanto può rappresentare la soluzione di molti problemi in situazioni poco chiare o disorientanti.  È possibile includere facilmente un sistema di Guida in un'applicazione per Windows utilizzando [Componente HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-windows-forms.md).  
  
## Tipi diversi di Guida  
 Il componente Windows Form <xref:System.Windows.Forms.HelpProvider> viene utilizzato per associare un file della Guida HTML Help 1.x all'applicazione Windows personalizzata, vale a dire un file CHM creato con HTML Help Workshop o un file HTM.  Il componente <xref:System.Windows.Forms.HelpProvider> può essere utilizzato per fornire una Guida sensibile al contesto per i controlli Windows Form o per controlli specifici.  Tramite il componente <xref:System.Windows.Forms.HelpProvider> è inoltre possibile aprire un file della Guida per aree specifiche, come la pagina principale di un sommario, un indice o una funzione di ricerca.  Per informazioni generali sul componente <xref:System.Windows.Forms.HelpProvider>, vedere [Cenni preliminari sul componente HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-overview-windows-forms.md).  Per informazioni su come utilizzare il componente <xref:System.Windows.Forms.HelpProvider> per visualizzare finestre popup della Guida in Windows Form, vedere [Procedura: visualizzare la Guida rapida](../../../../docs/framework/winforms/advanced/how-to-display-pop-up-help.md).  Per informazioni sull'utilizzo del componente <xref:System.Windows.Forms.ToolTip> per visualizzare finestre della Guida in linea specifiche per singoli controlli, vedere [Visualizzazione della Guida relativa a un controllo tramite le descrizioni comandi](../../../../docs/framework/winforms/advanced/control-help-using-tooltips.md).  
  
 È possibile generare file HTML Help 1.x utilizzando l'applicazione HTML Help Workshop.  Per ulteriori informazioni su HTML Help, vedere l'argomento "HTML Help Workshop" o gli argomenti relativi a "HTML Help" su MSDN.  
  
## Vedere anche  
 [Integrazione della Guida dell'utente in Windows Form](../../../../docs/framework/winforms/advanced/integrating-user-help-in-windows-forms.md)   
 [Componente HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-windows-forms.md)   
 [Componente ToolTip](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md)   
 [Panoramica sui Windows Form](../../../../docs/framework/winforms/windows-forms-overview.md)   
 [Windows Form](../../../../docs/framework/winforms/index.md)