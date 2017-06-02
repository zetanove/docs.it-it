---
title: "Procedura: raggruppare controlli RadioButton Windows Form in modo che funzionino come set | Microsoft Docs"
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
  - "controlli [Windows Form], raggruppamento"
  - "pulsanti di opzione, raggruppamento"
  - "RadioButton (controllo) [Windows Form], raggruppamento"
  - "controlli Windows Form, raggruppamento"
ms.assetid: 58f8fe34-50b7-49d8-a2be-c271be3c6b32
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: raggruppare controlli RadioButton Windows Form in modo che funzionino come set
I controlli <xref:System.Windows.Forms.RadioButton> Windows Form permettono all'utente di scegliere tra due o più impostazioni da assegnare a una routine o a un oggetto. È consentita l'assegnazione di una sola impostazione.  Ad esempio, all'interno di un gruppo di controlli <xref:System.Windows.Forms.RadioButton> che visualizzano una serie di corrieri a cui inoltrare un ordine è possibile utilizzare un solo corriere.  Si può quindi selezionare un solo <xref:System.Windows.Forms.RadioButton> alla volta, anche se fa parte di un gruppo funzionale.  
  
 È possibile raggruppare i pulsanti di opzione trascinandoli all'interno di un contenitore, ad esempio un controllo <xref:System.Windows.Forms.Panel>, un controllo <xref:System.Windows.Forms.GroupBox> o un form.  Tutti i pulsanti di opzione aggiunti direttamente a un form costituiscono un gruppo.  Per aggiungere gruppi separati è necessario inserirli all'interno di pannelli o di caselle di gruppo.  Per ulteriori informazioni su pannelli o caselle di gruppo, vedere [Cenni preliminari sul controllo Panel](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md) o [Cenni preliminari sul controllo GroupBox](../../../../docs/framework/winforms/controls/groupbox-control-overview-windows-forms.md).  
  
### Per raggruppare controlli RadioButton in modo che funzionino come un gruppo indipendente da altri gruppi  
  
1.  Trascinare sul form un controllo <xref:System.Windows.Forms.GroupBox> o <xref:System.Windows.Forms.Panel> dalla scheda **Windows Form** della **Casella degli strumenti**.  
  
2.  Trascinare i controlli <xref:System.Windows.Forms.RadioButton> sul controllo <xref:System.Windows.Forms.GroupBox> o <xref:System.Windows.Forms.Panel>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.RadioButton>   
 [Cenni preliminari sul controllo RadioButton](../../../../docs/framework/winforms/controls/radiobutton-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo Panel](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo GroupBox](../../../../docs/framework/winforms/controls/groupbox-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo CheckBox](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [Controllo RadioButton](../../../../docs/framework/winforms/controls/radiobutton-control-windows-forms.md)