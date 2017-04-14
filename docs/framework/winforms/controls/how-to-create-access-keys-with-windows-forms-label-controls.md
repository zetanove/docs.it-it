---
title: "Procedura: creare tasti di scelta con i controlli Label di Windows Form | Microsoft Docs"
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
  - "tasti di scelta, creazione per i controlli"
  - "tasti di scelta, Windows Form"
  - "controlli [Windows Form], tasti di scelta"
  - "controlli delle finestre di dialogo, tasti di scelta"
  - "tasti di scelta rapida, creazione per i controlli"
  - "Label (controllo) [Windows Form], creazione di tasti di scelta"
  - "tasti di scelta"
  - "tasti di scelta, aggiunta ai controlli delle finestre di dialogo"
  - "UseMnemonic (proprietà), Label (controllo)"
  - "controlli Windows Form, tasti di scelta"
ms.assetid: 5ee8f823-80be-4a4f-96a4-412671e2e306
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: creare tasti di scelta con i controlli Label di Windows Form
I controlli <xref:System.Windows.Forms.Label> di Windows Form possono essere utilizzati per definire tasti di scelta per altri controlli.  Quando si definisce un tasto di scelta in un controllo Label, si consente all'utente di spostare lo stato attivo al controllo successivo nell'ordine di tabulazione tramite la pressione contemporanea del tasto ALT e del tasto specificato.  Le etichette non possono ricevere lo stato attivo, che passa quindi automaticamente al controllo successivo nell'ordine di tabulazione.  Questa procedura può essere utilizzata per assegnare tasti di scelta a caselle di testo, caselle combinate, caselle di riepilogo e griglie dei dati.  
  
### Per assegnare un tasto di scelta a un controllo con un'etichetta  
  
1.  Creare prima l'etichetta, quindi l'altro controllo.  
  
     In alternativa  
  
     Creare i controlli in un ordine qualsiasi e impostare la proprietà <xref:System.Windows.Forms.Control.TabIndex%2A> dell'etichetta su un valore inferiore di uno rispetto a quello dell'altro controllo.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.Label.UseMnemonic%2A> dell'etichetta su `true`.  
  
3.  Nella proprietà <xref:System.Windows.Forms.Label.Text%2A> dell'etichetta utilizzare una e commerciale \(&\) per assegnare il tasto di scelta per l'etichetta.  Per ulteriori informazioni, vedere [Creazione di tasti di scelta per i controlli di Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md).  
  
    > [!NOTE]
    >  È possibile visualizzare le e commerciali in un controllo Label anziché utilizzarle per la creazione di tasti di scelta.  Ciò si verifica se si associa un controllo Label a un campo di un recordset in cui i dati includono e commerciali.  Per visualizzare le e commerciali in un controllo Label, impostare la proprietà <xref:System.Windows.Forms.Label.UseMnemonic%2A> su `false`.  Se si desidera visualizzare le e commerciali e disporre anche di un tasto di scelta, impostare la proprietà <xref:System.Windows.Forms.Label.UseMnemonic%2A> su `true`. Indicare quindi il tasto di scelta con una e commerciale \(&\) e la e commerciale da visualizzare con due e commerciali \(&&\).  
  
    ```vb  
    Label1.UseMnemonic = True  
    Label1.Text = "&Print"  
    Label2.UseMnemonic = True  
    Label2.Text = "&Copy && Paste"  
  
    ```  
  
    ```csharp  
    label1.UseMnemonic = true;  
    label1.Text = "&Print";  
    label2.UseMnemonic = true;  
    label2.Text = "&Copy && Paste";  
  
    ```  
  
    ```cpp  
    label1->UseMnemonic = true;  
    label1->Text = "&Print";  
    label2->UseMnemonic = true;  
    label2->Text = "&Copy && Paste";  
    ```  
  
## Vedere anche  
 [Procedura: ridimensionare un controllo Label Windows Form in base al contenuto](../../../../docs/framework/winforms/controls/how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)   
 [Cenni preliminari sul controllo Label](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)   
 [Controllo Label](../../../../docs/framework/winforms/controls/label-control-windows-forms.md)