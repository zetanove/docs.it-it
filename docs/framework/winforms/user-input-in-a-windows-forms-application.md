---
title: "User Input in a Windows Forms Application | Microsoft Docs"
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
  - "Windows Forms, user input"
ms.assetid: 9d61fa96-70f7-4754-885a-49a4a6316bdb
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# User Input in a Windows Forms Application
In Windows Form, l'input dell'utente viene inviato alle applicazioni sotto forma di messaggi di Windows.  Una serie di metodi sottoponibili a override elabora questi messaggi a livello di applicazione, form e controllo.  Quando questi metodi ricevono i messaggi dal mouse e dalla tastiera, generano eventi che è possibile gestire per ottenere informazioni sull'input del mouse o della tastiera.  In molti casi, le applicazioni Windows Form saranno in grado di elaborare tutti gli input dell'utente semplicemente gestendo questi eventi.  In altri casi, un'applicazione potrebbe richiedere l'override di uno dei metodi per l'elaborazione dei messaggi allo scopo di intercettare un messaggio specifico prima che venga ricevuto dall'applicazione, dal form o dal controllo.  
  
## Eventi di mouse e tastiera  
 Tutti i controlli Windows Form ereditano un gruppo di eventi correlati all'input del mouse e della tastiera.  Ad esempio, un controllo può gestire l'evento <xref:System.Windows.Forms.Control.KeyPress> per determinare il codice carattere di un tasto premuto. Oppure, un controllo può gestire l'evento <xref:System.Windows.Forms.Control.MouseClick> per determinare la posizione di un clic del mouse.  Per ulteriori informazioni sugli eventi di mouse e tastiera, vedere [Using Keyboard Events](../../../docs/framework/winforms/using-keyboard-events.md) e [Mouse Events in Windows Forms](../../../docs/framework/winforms/mouse-events-in-windows-forms.md).  
  
## Metodi per l'elaborazione dei messaggi di input dell'utente  
 Form e controlli hanno accesso all'interfaccia di <xref:System.Windows.Forms.IMessageFilter> e a un gruppo di metodi sottoponibili a override che elaborano i messaggi di Windows in punti diversi della coda messaggi.  Questi metodi includono tutti un parametro <xref:System.Windows.Forms.Message>, che incapsula i dettagli a basso livello dei messaggi di Windows.  È possibile implementare o sottoporre a override questi metodi per esaminare e quindi eseguire il messaggio, oppure passarlo al consumer successivo nella coda messaggi.  Nella tabella seguente vengono illustrati i metodi che elaborano tutti i messaggi di Windows in Windows Form.  
  
|Metodo|Note|  
|------------|----------|  
|<xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A>|Il metodo intercetta i messaggi di Windows in coda \(o inseriti\) a livello di applicazione.|  
|<xref:System.Windows.Forms.Control.PreProcessMessage%2A>|Il metodo intercetta i messaggi di Windows a livello di form e di controllo prima che siano elaborati.|  
|<xref:System.Windows.Forms.Control.WndProc%2A>|Il metodo intercetta i messaggi di Windows a livello di form e di controllo.|  
|<xref:System.Windows.Forms.Control.DefWndProc%2A>|Il metodo esegue l'elaborazione predefinita dei messaggi di Windows a livello di form e di controllo.  Offre la funzionalità minima di una finestra.|  
|<xref:System.Windows.Forms.Control.OnNotifyMessage%2A>|Il metodo intercetta i messaggi a livello di form e di controllo dopo che sono stati elaborati.  Perché venga chiamato questo metodo, il bit di stile <xref:System.Windows.Forms.ControlStyles> deve essere impostato.|  
  
 I messaggi di tastiera e mouse vengono inoltre elaborati da un gruppo aggiuntivo di metodi sottoponibili a override specifici di questi tipi di messaggi.  Per ulteriori informazioni, vedere [How Keyboard Input Works](../../../docs/framework/winforms/how-keyboard-input-works.md) e [How Mouse Input Works in Windows Forms](../../../docs/framework/winforms/how-mouse-input-works-in-windows-forms.md).  
  
## Vedere anche  
 [User Input in Windows Forms](../../../docs/framework/winforms/user-input-in-windows-forms.md)   
 [Keyboard Input in a Windows Forms Application](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)   
 [Mouse Input in a Windows Forms Application](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)