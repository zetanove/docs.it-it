---
title: "Procedura: supportare l&#39;interoperabilit&#224; COM visualizzando un Windows Form con il metodo ShowDialog | Microsoft Docs"
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
  - "COM [Windows Form]"
  - "Windows Form, non gestito"
  - "interoperabilità COM, chiamata di metodi"
  - "controlli ActiveX [Windows Form], interoperabilità COM"
  - "ShowDialog (metodo)"
  - "Windows Form, interoperabilità"
ms.assetid: 87aac8ad-3c04-43b3-9b0c-d0b00df9ee74
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: supportare l&#39;interoperabilit&#224; COM visualizzando un Windows Form con il metodo ShowDialog
È possibile risolvere i problemi di interoperabilità di Component Object Model \(COM\) visualizzando il Windows Form in un ciclo di messaggi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] creato usando il metodo <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName>.  
  
 Per fare in modo che un form funzioni correttamente da un'applicazione client COM, è necessario eseguirlo in un ciclo di messaggi Windows Form. Per eseguire questa operazione, adottare uno degli approcci seguenti:  
  
-   Usare il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> per visualizzare il Windows Form.  
  
-   Visualizzare ogni Windows Form in un thread separato. Per altre informazioni, vedere [Procedura: supportare l'interoperabilità COM mediante la visualizzazione di ogni Windows Form nel relativo thread](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md).  
  
## Routine  
 Il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> può offrire la soluzione più semplice per visualizzare un form in un ciclo di messaggi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] poiché, di tutti gli approcci, è quello che richiede l'implementazione della minore quantità di codice.  
  
 Il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> sospende il ciclo di messaggi dell'applicazione non gestita e visualizza il form come una finestra di dialogo. Poiché il ciclo di messaggi dell'applicazione host è stato sospeso, il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> crea un nuovo ciclo di messaggi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per elaborare i messaggi del form.  
  
 Lo svantaggio dell'uso del metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> consiste nel fatto che il form viene aperto come finestra di dialogo modale. Questo comportamento blocca eventuali interfacce utente \(UI\) nell'applicazione chiamante mentre il Windows Form è aperto. Quando l'utente esce dal form, il ciclo di messaggi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] si chiude e il ciclo di messaggi dell'applicazione precedente viene eseguito di nuovo.  
  
 È possibile creare una libreria di classi in Windows Form che dispone di un metodo per visualizzare il form e quindi compilare la libreria di classi per l'interoperabilità COM. È possibile usare questo file DLL da Visual Basic 6.0 o Microsoft Foundation Classes \(MFC\) e da uno dei due ambienti è possibile chiamare il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> per visualizzare il form.  
  
#### Per supportare l'interoperabilità COM visualizzando un Windows Form con il metodo ShowDialog  
  
-   Sostituire tutte le chiamate al metodo <xref:System.Windows.Forms.Form.Show%2A?displayProperty=fullName> con chiamate al metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> nel componente [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
## Vedere anche  
 [Exposing .NET Framework Components to COM](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [Procedura: supportare l'interoperabilità COM mediante la visualizzazione di ogni Windows Form nel relativo thread](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)   
 [Windows Forms and Unmanaged Applications](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)