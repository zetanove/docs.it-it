---
title: "Procedura: visualizzare la Guida rapida | Microsoft Docs"
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
  - "F1 (Guida), in finestre di dialogo"
  - "form, visualizzazione della Guida"
  - "Guida, aggiunta a finestre di dialogo"
  - "Guida, Guida rapida"
  - "HelpProvider (componente) [Windows Form]"
  - "finestre di dialogo modali, Guida rapida"
  - "Guida rapida"
  - "Windows Form, visualizzazione della Guida"
ms.assetid: 218aa81e-e87e-4d67-af05-11627bbdce3b
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: visualizzare la Guida rapida
Per visualizzare la Guida in Windows Form, è possibile fare clic sul pulsante **?** sulla destra della barra del titolo, accessibile dalla proprietà <xref:System.Windows.Forms.Form.HelpButton%2A>.  Questo tipo di visualizzazione della Guida è ideale con le finestre di dialogo.  Con le finestre di dialogo visualizzate come modali \(con il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A>\) risulta difficile accedere a sistemi di Guida esterni, perché le finestre di dialogo modali devono venire chiuse prima che lo stato attivo possa passare a un'altra finestra.  Inoltre, per poter usare il pulsante **?**, sulla barra del titolo non devono essere presenti pulsanti **Riduci a icona** o **Ingrandisci**.  Questa è una convenzione delle finestre di dialogo standard, a differenza dei form in cui in genere sono presenti i pulsanti **Riduci a icona** e **Ingrandisci**.  
  
 Tenere presente che è possibile usare anche il componente <xref:System.Windows.Forms.HelpProvider> per collegare i controlli ai file in un sistema di Guida, anche se è stata implementata la Guida rapida.  Per altre informazioni, vedere [Visualizzazione della Guida in un'applicazione Windows](../../../../docs/framework/winforms/advanced/how-to-provide-help-in-a-windows-application.md).  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per visualizzare la Guida rapida  
  
1.  Trascinare un componente [HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-windows-forms.md) dalla casella degli strumenti al form.  
  
     Il componente verrà posizionato sulla barra delle applicazioni in basso in Progettazione Windows Form.  
  
2.  Nella finestra Proprietà impostare la proprietà <xref:System.Windows.Forms.Form.HelpButton%2A> su `true`.  Sulla destra della barra del titolo del form verrà visualizzato un pulsante con un punto interrogativo.  
  
3.  Per visualizzare <xref:System.Windows.Forms.Form.HelpButton%2A>, è necessario impostare le proprietà <xref:System.Windows.Forms.Form.MinimizeBox%2A> e <xref:System.Windows.Forms.Form.MaximizeBox%2A> del form su `false`, la proprietà <xref:System.Windows.Forms.Form.ControlBox%2A> su `true` e la proprietà <xref:System.Windows.Forms.Form.FormBorderStyle%2A> su uno dei valori seguenti: <xref:System.Windows.Forms.FormBorderStyle>, <xref:System.Windows.Forms.FormBorderStyle>, <xref:System.Windows.Forms.FormBorderStyle> o <xref:System.Windows.Forms.FormBorderStyle>.  
  
4.  Selezionare il controllo per il quale si desidera visualizzare la Guida nel form e impostare la stringa della Guida nella finestra Proprietà.  Questa è la stringa di testo che verrà visualizzata in una finestra simile a un [ToolTip](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md).  
  
5.  Premere **F5**.  
  
6.  Premere il pulsante **?** sulla barra del titolo e fare clic sul controllo per cui è stata impostata la stringa della Guida.  
  
## Vedere anche  
 [Visualizzazione della Guida relativa a un controllo tramite le descrizioni comandi](../../../../docs/framework/winforms/advanced/control-help-using-tooltips.md)   
 [Integrazione della Guida dell'utente in Windows Form](../../../../docs/framework/winforms/advanced/integrating-user-help-in-windows-forms.md)   
 [Windows Form](../../../../docs/framework/winforms/index.md)