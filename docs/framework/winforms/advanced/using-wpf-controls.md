---
title: "Utilizzo di controlli WPF | Microsoft Docs"
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
  - "interoperabilità [WPF]"
  - "Progettazione Windows Form, interoperabilità con WPF"
ms.assetid: 03c85dce-26ad-44cd-bc1d-8e0cb56de096
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Utilizzo di controlli WPF
È possibile utilizzare i controlli Windows Presentation Foundation \(WPF\) nelle applicazioni basate su Windows Form  Benché queste due tecnologie di visualizzazione siano diverse, si integrano perfettamente.  
  
 Progettazione Windows Form include un ambiente di progettazione visivo per includere i controlli Windows Presentation Foundation.  Un controllo WPF è ospitato da uno speciale controllo Windows Forms denominato <xref:System.Windows.Forms.Integration.ElementHost>.  Questo controllo consente al controllo WPF di partecipare al layout del form e ricevere i messaggi della tastiera e del mouse.  In fase di progettazione è possibile disporre il controllo <xref:System.Windows.Forms.Integration.ElementHost> come qualsiasi altro controllo Windows Form.  
  
 È inoltre possibile utilizzare i controlli Windows Form nelle applicazioni WPF.  Per ulteriori informazioni, vedere [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26).  
  
## In questa sezione  
 [Procedura: copiare e incollare un controllo ElementHost in fase di progettazione](../../../../docs/framework/winforms/advanced/how-to-copy-and-paste-an-elementhost-control-at-design-time.md)  
 Viene illustrato come copiare un controllo Windows Presentation Foundation in un Windows Form  
  
 [Procedura dettagliata: disposizione del contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-arranging-wpf-content-on-windows-forms-at-design-time.md)  
 Viene illustrato come utilizzare le funzionalità del layout di Windows Form, ad esempio l'ancoraggio e le guide di allineamento, per disporre i controlli di Windows Presentation Foundation.  
  
 [Procedura dettagliata: modifica delle proprietà di un elemento WPF ospitato in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-changing-properties-of-a-hosted-wpf-element-at-design-time.md)  
 Viene illustrato il flusso di lavoro tra Progettazione Windows Form e  [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] per la modifica delle proprietà sui controlli WPF.  
  
 [Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)  
 Viene illustrato come creare un controllo Windows Presentation Foundation per l'utilizzo nelle applicazioni basate su Windows Form.  
  
 [Procedura dettagliata: copiare e incollare un controllo ElementHost in Windows Form separati](../../../../docs/framework/winforms/advanced/copy--paste-an-elementhost-control-into-forms.md)  
 Viene illustrato come copiare un controllo Windows Presentation Foundation da un Windows Form a un altro.  
  
 [Procedura dettagliata: assegnazione del contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-assigning-wpf-content-on-windows-forms-at-design-time.md)  
 Viene illustrato come selezionare i tipi di controlli Windows Presentation Foundation che si desidera visualizzare sul form.  
  
 [Procedura dettagliata: applicazione di stili al contenuto WPF](../../../../docs/framework/winforms/advanced/walkthrough-styling-wpf-content.md)  
 Viene illustrato il flusso di lavoro tra Progettazione Windows Form e [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)] per l'applicazione degli stili ai controlli Windows Presentation Foundation.  
  
## Riferimenti  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 Viene descritta una classe che consente di includere i controlli Windows Presentation Foundation nelle applicazioni basate su Windows Form  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 Viene descritta una classe che consente di includere i controlli Windows Form nell'applicazione basata su Windows Presentation Foundation  
  
## Sezioni correlate  
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)  
 Viene descritta l'interazione tra le tecnologie di Windows Presentation Foundation e Windows Form.  
  
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)  
 Viene descritto come progettare controlli Windows Presentation Foundation in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].