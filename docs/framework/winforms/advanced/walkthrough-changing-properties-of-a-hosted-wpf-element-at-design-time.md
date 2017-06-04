---
title: "Procedura dettagliata: modifica delle propriet&#224; di un elemento WPF ospitato in fase di progettazione | Microsoft Docs"
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
  - "Windows Form, modifica delle proprietà di contenuti WPF in fase di progettazione"
  - "contenuto WPF [Windows Form], modifica di proprietà in fase di progettazione"
  - "contenuto WPF, hosting in Windows Form"
ms.assetid: a1f7a90c-0bbb-4781-8c3c-8cc8bef2488d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura dettagliata: modifica delle propriet&#224; di un elemento WPF ospitato in fase di progettazione
Questa procedura dettagliata mostra come cambiare i valori delle proprietà di un controllo Windows Presentation Foundation \(WPF\) incluso in un Windows Form.  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creare il progetto.  
  
-   Creare il controllo WPF.  
  
-   Inserire i controlli WPF in Windows Form  
  
-   Usare WPF Designer per Visual Studio per cambiare i valori delle proprietà.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)].  
  
## Creazione del progetto  
 Il primo passaggio consiste nella creazione del progetto Windows Form.  
  
> [!NOTE]
>  Con il contenuto WPF sono supportati solo progetti C\# e Visual Basic.  
  
#### Per creare il progetto  
  
-   Creare un nuovo progetto di applicazione Windows Form in Visual Basic o Visual C\# denominato `WpfHost`.  
  
## Creazione del controllo WPF  
 Dopo avere aggiunto un controllo WPF al progetto, è possibile disporlo sul form.  
  
#### Per creare controlli WPF  
  
1.  Aggiungere un nuovo <xref:System.Windows.Controls.UserControl> WPF al progetto.  Usare il nome predefinito per il tipo di controllo, `UserControl1.xaml`.  Per altre informazioni, vedere [Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).  
  
2.  Nella finestra **Proprietà** impostare il valore della proprietà <xref:System.Windows.Controls.Control.Background%2A> su `Blue`.  
  
3.  Compilare il progetto.  
  
## Modifica dei valori delle proprietà nel controllo WPF  
 Lo smart tag <xref:System.Windows.Forms.Integration.ElementHost> facilita la modifica delle proprietà del contenuto WPF ospitato usando WPF Designer.  
  
#### Per includere un controllo WPF  
  
1.  Aprire `Form1` in Progettazione Windows Form.  
  
2.  Nella **Casella degli strumenti** della scheda **Controlli utente WPF** fare doppio clic su `UserControl1` per creare un'istanza di `UserControl1` nel form.  
  
     L'istanza di `UserControl1` viene inclusa in un nuovo controllo <xref:System.Windows.Forms.Integration.ElementHost> denominato `elementHost1`.  
  
3.  Nel pannello smart tag **ElementHost Tasks** selezionare **Modifica contenuto ospitato**.  
  
     UserControl1.xaml viene aperto in WPF Designer.  
  
4.  Nella finestra **Proprietà** impostare il valore della proprietà <xref:System.Windows.Controls.Control.Background%2A> su `Red`.  
  
5.  Ricompilare il progetto.  
  
6.  Aprire `Form1` in Progettazione Windows Form.  
  
     L'istanza di `UserControl1` presenta uno sfondo rosso.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [Procedura: allineare un controllo ai bordi dei form in fase di progettazione](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [Utilizzo di controlli WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)