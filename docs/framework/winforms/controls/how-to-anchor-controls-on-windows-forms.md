---
title: "Procedura: agganciare i controlli in Windows Form | Microsoft Docs"
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
  - "Anchor (proprietà), abilitazione di form ridimensionabili"
  - "controlli [Windows Form], ancoraggio"
  - "controlli [Windows Form], posizionamento"
  - "form, ridimensionamento"
  - "ridimensionamento di form"
  - "risoluzione dello schermo e visualizzazione controlli"
  - "controlli Windows Form, risoluzioni dello schermo"
  - "controlli Windows Form, dimensione"
  - "Windows Form, ridimensionamento"
ms.assetid: 59ea914f-fbd3-427a-80fe-decd02f7ae6d
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: agganciare i controlli in Windows Form
Se si sta progettando un form ridimensionabile dall'utente in fase di esecuzione, è necessario che i controlli nel form vengano ridimensionati e riposizionati correttamente.  Per ridimensionare i controlli dinamicamente con il form, è possibile utilizzare la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> dei controlli per Windows Form.  La proprietà <xref:System.Windows.Forms.Control.Anchor%2A> definisce una posizione di aggancio per il controllo.  Quando un controllo viene agganciato a un form e il form viene ridimensionato, il controllo mantiene la distanza tra il controllo e le posizioni di aggancio.  Se, ad esempio, un controllo <xref:System.Windows.Forms.TextBox> è agganciato al bordo sinistro, al bordo destro e al bordo inferiore del form, quando quest'ultimo viene ridimensionato, il controllo <xref:System.Windows.Forms.TextBox> viene a sua volta ridimensionato orizzontalmente, in modo che si trovi alla stessa distanza dai lati destro e sinistro del form.  Il controllo si colloca inoltre verticalmente, per mantenere la propria posizione alla medesima distanza dal bordo inferiore del form.  Se un controllo non è agganciato e il form viene ridimensionato, la posizione del controllo rispetto ai bordi del form risulterà modificata.  
  
 La proprietà <xref:System.Windows.Forms.Control.Anchor%2A> interagisce con la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A>.  Per ulteriori informazioni, vedere [Cenni preliminari sulla proprietà AutoSize](../../../../docs/framework/winforms/controls/autosize-property-overview.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per agganciare un controllo in un form  
  
1.  Selezionare il controllo che si desidera agganciare.  
  
    > [!NOTE]
    >  Per agganciare più controlli contemporaneamente, tenere premuto il tasto CTRL e selezionare i controlli desiderati, quindi seguire la procedura descritta.  
  
2.  Nella finestra **Proprietà** fare clic sulla freccia a destra della proprietà <xref:System.Windows.Forms.Control.Anchor%2A>.  
  
     Viene visualizzato un editor con una croce.  
  
3.  Per impostare un aggancio fare clic nella sezione superiore, sinistra, destra o inferiore della croce.  
  
     In base all'impostazione predefinita, i controlli vengono agganciati nella parte superiore e a sinistra.  
  
4.  Per deselezionare un lato del controllo che è stato agganciato, fare clic sulla parte corrispondente della croce.  
  
5.  Fare nuovamente clic sul nome della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> per chiudere il relativo editor.  
  
 Quando il form viene visualizzato in fase di esecuzione, il controllo viene ridimensionato per rimanere posizionato alla stessa distanza dal bordo del form.  La distanza dal bordo agganciato resta sempre uguale alla distanza definita quando il controllo viene posizionato in Progettazione Windows Form.  
  
> [!NOTE]
>  Alcuni controlli, ad esempio <xref:System.Windows.Forms.ComboBox>, presentano un'altezza limitata.  L'aggancio del controllo nella parte inferiore del form o del contenitore non ha alcun effetto sul limite dell'altezza del controllo, che non può essere superato.  
  
 I controlli ereditati, per poter essere agganciati, devono essere `Protected`.  Per modificare il livello di accesso di un controllo, impostare la proprietà `Modifiers` nella finestra **Proprietà**.  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Cenni preliminari sulla proprietà AutoSize](../../../../docs/framework/winforms/controls/autosize-property-overview.md)   
 [Procedura: ancorare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando FlowLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [Procedura dettagliata: disposizione di controlli Windows Form utilizzando spaziatura, margini e la proprietà AutoSize](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md)