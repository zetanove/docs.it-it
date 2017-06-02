---
title: "Procedura: creare un&#39;interfaccia di tipo Esplora risorse in un Windows Form | Microsoft Docs"
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
  - "form, Windows Explorer (tipo)"
  - "SplitContainer (controllo) [Windows Form], interfaccia di tipo Esplora risorse"
  - "Esplora risorse, creazione con Windows Form"
ms.assetid: 9a3d5f4f-5dda-4350-9ad5-57ce5976dc47
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: creare un&#39;interfaccia di tipo Esplora risorse in un Windows Form
In molte applicazioni viene scelto di utilizzare un'interfaccia analoga a quella di Esplora risorse, poiché è ormai familiare a tutti gli utenti.  
  
 L'interfaccia di Esplora risorse è costituita essenzialmente da un controllo <xref:System.Windows.Forms.TreeView> e da un controllo <xref:System.Windows.Forms.ListView>, situati in due pannelli separati  ridimensionabili tramite una barra di divisione.  Questa disposizione dei controlli è particolarmente efficace per la visualizzazione e la ricerca di informazioni.  
  
 La procedura che segue illustra come disporre i controlli in un form di tipo Esplora risorse,  ma non spiega come aggiungere la funzionalità di esplorazione file dell'applicazione Esplora risorse.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un Windows Form di tipo Esplora risorse  
  
1.  Creare un nuovo progetto applicazione Windows.  Per informazioni dettagliate, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Dalla **Casella degli strumenti**:  
  
    1.  Trascinare un controllo <xref:System.Windows.Forms.SplitContainer> sul form.  
  
    2.  Trascinare un controllo <xref:System.Windows.Forms.TreeView> nel pannello **SplitterPanel1**, ovvero il pannello del controllo <xref:System.Windows.Forms.SplitContainer> contrassegnato come **Panel1**.  
  
    3.  Trascinare un controllo <xref:System.Windows.Forms.ListView> nel pannello **SplitterPanel2**, ovvero il pannello del controllo <xref:System.Windows.Forms.SplitContainer> contrassegnato come **Panel2**.  
  
3.  Selezionare tutti e tre i controlli premendo il tasto CTRL e facendo clic su ciascun controllo.  Per selezionare il controllo <xref:System.Windows.Forms.SplitContainer>, fare clic sulla barra di divisione e non sui pannelli.  
  
    > [!NOTE]
    >  Non utilizzare il comando **Seleziona tutto** dal menu **Modifica**.  Se si utilizza tale comando, infatti, la proprietà necessaria per il passaggio successivo non verrà visualizzata nella finestra **Proprietà**.  
  
4.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
5.  ‎Premere F5 per eseguire l'applicazione.  
  
     Nel form viene visualizzata un'interfaccia in due parti, analoga a quella di Esplora risorse.  
  
    > [!NOTE]
    >  Quando si trascina la barra di divisione, i pannelli vengono ridimensionati.  
  
## Vedere anche  
 <xref:System.Windows.Forms.SplitContainer>   
 [Procedura: creare un'interfaccia utente a più riquadri con Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-multipane-user-interface-with-windows-forms.md)   
 [Procedura: definire il ridimensionamento e il posizionamento in una finestra divisa](../../../../docs/framework/winforms/controls/how-to-define-resize-and-positioning-behavior-in-a-split-window.md)   
 [Procedura: suddividere una finestra orizzontalmente](../../../../docs/framework/winforms/controls/how-to-split-a-window-horizontally.md)   
 [Controllo SplitContainer](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)