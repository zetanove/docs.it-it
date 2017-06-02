---
title: "Order of Events in Windows Forms | Microsoft Docs"
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
  - "events [Windows Forms], order of"
  - "focus event order"
  - "application shutdown event order"
  - "sequence, of events"
  - "validation events, order of"
  - "application startup event order"
ms.assetid: e81db09b-4453-437f-b78a-62d7cd5c9829
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Order of Events in Windows Forms
L'ordine in cui gli eventi vengono generati nelle applicazioni Windows Form è di particolare interesse per gli sviluppatori interessati alla gestione di ciascuno di questi eventi a turno.  Quando una situazione richiede una precisa gestione degli eventi, ad esempio quando si riprogettano parti del form, è necessaria la conoscenza dell'ordine esatto in cui vengono generati gli eventi in fase di esecuzione.  Questo argomento contiene alcune informazioni dettagliate sull'ordine degli eventi durante le varie fasi importanti nella durata delle applicazioni e dei controlli.  Per informazioni specifiche sull'ordine degli eventi di input del mouse, vedere [Mouse Events in Windows Forms](../../../docs/framework/winforms/mouse-events-in-windows-forms.md).  Per una panoramica degli eventi in Windows Form, vedere [Events Overview](../../../docs/framework/winforms/events-overview-windows-forms.md).  Per informazioni dettagliate sulla creazione di gestori eventi, vedere [Event Handlers Overview](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md).  
  
## Eventi di arresto e avvio dell'applicazione  
 Le classi<xref:System.Windows.Forms.Form> e <xref:System.Windows.Forms.Control> espongono un set di eventi correlati all'avvio e all'arresto dell'applicazione.  Quando si avvia un'applicazione Windows Form, gli eventi di avvio del form principale vengono generati nell'ordine seguente:  
  
-   <xref:System.Windows.Forms.Control.HandleCreated?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Control.BindingContextChanged?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Load?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Control.VisibleChanged?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Activated?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Shown?displayProperty=fullName>  
  
 Quando un'applicazione viene chiusa, gli eventi di chiusura del form principale vengono generati nell'ordine seguente:  
  
-   <xref:System.Windows.Forms.Form.Closing?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.FormClosing?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Closed?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.FormClosed?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.Form.Deactivate?displayProperty=fullName>  
  
 L'evento <xref:System.Windows.Forms.Application.ApplicationExit> della classe <xref:System.Windows.Forms.Application> viene generato dopo gli eventi di chiusura del form principale.  
  
> [!NOTE]
>  Visual Basic 2005 include eventi di applicazioni aggiuntivi, come <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup?displayProperty=fullName> e <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown?displayProperty=fullName>.  
  
## Eventi di convalida e relativi allo stato attivo  
 Quando si modifica lo stato attivo usando la tastiera \(TAB, MAIUSC \+ TAB e così via\), chiamando i metodi <xref:System.Windows.Forms.Control.Select%2A> o <xref:System.Windows.Forms.Control.SelectNextControl%2A> oppure impostando la proprietà <xref:System.Windows.Forms.ContainerControl.ActiveControl%2A> sul form corrente, gli eventi di attivazione della classe <xref:System.Windows.Forms.Control> si verificano nell'ordine seguente:  
  
-   <xref:System.Windows.Forms.Control.Enter>  
  
-   <xref:System.Windows.Forms.Control.GotFocus>  
  
-   <xref:System.Windows.Forms.Control.Leave>  
  
-   <xref:System.Windows.Forms.Control.Validating>  
  
-   <xref:System.Windows.Forms.Control.Validated>  
  
-   <xref:System.Windows.Forms.Control.LostFocus>  
  
 Quando si modifica lo stato attivo usando il mouse o chiamando il metodo <xref:System.Windows.Forms.Control.Focus%2A>, gli eventi di attivazione della classe <xref:System.Windows.Forms.Control> si verificano nell'ordine seguente:  
  
-   <xref:System.Windows.Forms.Control.Enter>  
  
-   <xref:System.Windows.Forms.Control.GotFocus>  
  
-   <xref:System.Windows.Forms.Control.LostFocus>  
  
-   <xref:System.Windows.Forms.Control.Leave>  
  
-   <xref:System.Windows.Forms.Control.Validating>  
  
-   <xref:System.Windows.Forms.Control.Validated>  
  
## Vedere anche  
 [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)