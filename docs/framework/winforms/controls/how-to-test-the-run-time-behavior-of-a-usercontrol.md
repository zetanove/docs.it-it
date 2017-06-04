---
title: "Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl | Microsoft Docs"
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
  - "controlli composti, test"
  - "controlli utente [Windows Form], test"
  - "UserControl (classe), comportamento di runtime"
  - "UserControl (classe), test"
  - "UserControl Test Container"
ms.assetid: 4e4d5c49-1346-40ac-9d96-40211b573583
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl
Quando si sviluppa un controllo <xref:System.Windows.Forms.UserControl>, è necessario eseguirne il test del comportamento in fase di esecuzione.  È possibile creare un distinto progetto di applicazione basata su Windows e inserire il controllo in un form di test, anche se questa non è la procedura più efficiente.  Un modo più rapido e semplice consiste nell'utilizzo dello strumento **UserControl Test Container** fornito da Visual Studio,  avviandolo direttamente dal progetto Libreria di controlli Windows.  
  
> [!IMPORTANT]
>  Il controllo <xref:System.Windows.Forms.UserControl> deve disporre di almeno un costruttore pubblico per potere essere caricato da Test Container.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
> [!NOTE]
>  Non è possibile testare il controllo Visual C\+\+ utilizzando **UserControl Test Container**.  
  
### Per eseguire il test del comportamento in fase di esecuzione del controllo UserControl  
  
1.  Creare un progetto Libreria di controlli Windows denominato EsempioTestContainer.  Per informazioni dettagliate, vedere [Windows Control Library Template](http://msdn.microsoft.com/it-it/722f4e2d-1310-4ed5-8f33-593337ab66b4).  
  
2.  In **Progettazione Windows Form** trascinare un controllo <xref:System.Windows.Forms.Label> dalla **Casella degli strumenti** nell'area di progettazione del controllo.  
  
3.  Premere F5 per compilare il progetto ed eseguire **UserControl Test Container**.  Nel riquadro **Anteprima** verrà visualizzato lo strumento Test Container con il controllo <xref:System.Windows.Forms.UserControl>.  
  
4.  Selezionare la proprietà <xref:System.Windows.Forms.Control.BackColor%2A> visualizzata nel controllo <xref:System.Windows.Forms.PropertyGrid> a destra del riquadro **Anteprima**.  Modificare il valore in `ControlDark`.  Si noti che il colore del controllo diventa più scuro.  Provare a modificare altri valori di proprietà e notare l'effetto sul controllo.  
  
5.  Selezionare la casella di controllo **Controllo utente Dock Fill** sotto il riquadro **Anteprima**.  Si noti che il controllo viene ridimensionato in modo da occupare il riquadro.  Ridimensionare Test Container e notare che il controllo viene ridimensionato con il riquadro.  
  
6.  Chiudere Test Container.  
  
7.  Aggiungere un altro controllo utente al progetto EsempioTestContainer.  Per informazioni dettagliate, vedere [NIB:How to: Add Existing Items to a Project](http://msdn.microsoft.com/it-it/15f4cfb7-78ab-457f-9f14-099a25a6a2d3).  
  
8.  In **Progettazione Windows Form** trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nell'area di progettazione del controllo.  
  
9. Premere F5 per compilare il progetto ed eseguire Test Container.  
  
10. Fare clic sul controllo <xref:System.Windows.Forms.ComboBox> **Seleziona controllo utente** per alternare tra i due controlli utente.  
  
## Test di controlli utente contenuti in un altro progetto  
 È possibile eseguire il test di controlli utente contenuti in altri progetti nello strumento Test Container del progetto corrente.  
  
#### Per eseguire il test di controlli utente contenuti in un altro progetto  
  
1.  Creare un progetto Libreria di controlli Windows denominato EsempioTestContainer2.  Per informazioni dettagliate, vedere [Windows Control Library Template](http://msdn.microsoft.com/it-it/722f4e2d-1310-4ed5-8f33-593337ab66b4).  
  
2.  In **Progettazione Windows Form** trascinare un controllo <xref:System.Windows.Forms.RadioButton> dalla **Casella degli strumenti** nell'area di progettazione del controllo.  
  
3.  Premere F5 per compilare il progetto ed eseguire Test Container.  Nel riquadro **Anteprima** verrà visualizzato lo strumento Test Container con il controllo <xref:System.Windows.Forms.UserControl>.  
  
4.  Fare clic sul pulsante **Carica**.  
  
5.  Nella finestra di dialogo **Apri** individuare il file EsempioTestContainer.dll compilato durante la procedura precedente.  Selezionare EsempioTestContainer.dll e scegliere **Apri** per caricare i controlli utente.  
  
6.  Utilizzare il controllo <xref:System.Windows.Forms.ComboBox> **Seleziona controllo utente** per alternare tra i due controlli utente contenuti nel progetto EsempioTestContainer.  
  
## Vedere anche  
 <xref:System.Windows.Forms.UserControl>   
 [Procedura: modificare controlli compositi](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md)   
 [Procedura dettagliata: modifica di un controllo composito con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [Procedura dettagliata: modifica di un controllo composito con Visual C\#](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)   
 [User Control Designer](http://msdn.microsoft.com/it-it/2abb9eec-ba32-45cb-b73d-8b52a8bd6bf1)