---
title: "Procedura: raggruppare i controlli con il controllo Panel di Windows Form nella finestra di progettazione | Microsoft Docs"
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
  - "Panel (controllo) [Windows Form], raggruppamento di controlli"
  - "controlli Windows Form, raggruppamento"
ms.assetid: 7e1cd708-fdb1-49d8-9ca2-5640b276bf2e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: raggruppare i controlli con il controllo Panel di Windows Form nella finestra di progettazione
I controlli <xref:System.Windows.Forms.Panel> di Windows Form vengono utilizzati per raggruppare altri controlli.  Il raggruppamento dei controlli risulta utile per tre motivi:  ai fini del raggruppamento visivo di elementi di form per la realizzazione di un'interfaccia utente chiara e intuitiva, per il raggruppamento a livello di programmazione, ad esempio di pulsanti di opzione, infine per poter spostare i controlli in blocco in fase di progettazione.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un gruppo di controlli  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.Panel> dalla scheda **Windows Form** della casella degli strumenti in un form.  
  
2.  Aggiungere al pannello altri controlli, creando ciascun controllo all'interno del pannello.  
  
     Se si desidera inserire in un pannello controlli esistenti, è possibile selezionarli e tagliarli, selezionare il controllo <xref:System.Windows.Forms.Panel>, quindi incollare i controlli nella casella di gruppo.  È anche possibile trascinare i controlli nel pannello.  
  
3.  Se si desidera aggiungere un bordo a un pannello, impostare la proprietà <xref:System.Windows.Forms.BorderStyle> del pannello \(facoltativo\).  Sono disponibili tre scelte: <xref:System.Windows.Forms.BorderStyle>, <xref:System.Windows.Forms.BorderStyle> e <xref:System.Windows.Forms.BorderStyle>.  
  
## Vedere anche  
 [Controllo Panel](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)   
 [Cenni preliminari sul controllo Panel](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [Procedura: impostare lo sfondo di un controllo Panel](../../../../docs/framework/winforms/controls/how-to-set-the-background-of-a-windows-forms-panel.md)