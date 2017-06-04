---
title: "Procedura dettagliata: disposizione del contenuto WPF in Windows Form in fase di progettazione | Microsoft Docs"
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
  - "Windows Form, ancoraggio di contenuto WPF"
  - "Windows Form, disposizione di contenuti WPF in fase di progettazione"
  - "contenuto WPF [Windows Form], disposizione in fase di progettazione"
  - "contenuto WPF, hosting in Windows Form"
  - "controllo utenti WPF [Windows Form], hosting in un pannello del layout"
ms.assetid: 5efb1c53-1484-43d6-aa8a-f4861b99bb8a
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Procedura dettagliata: disposizione del contenuto WPF in Windows Form in fase di progettazione
Questa procedura dettagliata illustra come usare le funzionalità di layout di Windows Form, ad esempio l'ancoraggio e le guide di allineamento, per disporre i controlli di Windows Presentation Foundation \(WPF\).  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creare il progetto.  
  
-   Creare il controllo WPF.  
  
-   Ospitare i controlli WPF in un pannello di layout.  
  
-   Allineare i controlli WPF mediante le guide di allineamento.  
  
-   Ancorare e agganciare i controlli WPF.  
  
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
  
-   Creare un nuovo progetto di applicazione Windows Form in Visual Basic o Visual C\# denominato `ArrangeElementHost`.  
  
## Creazione del controllo WPF  
 Dopo avere aggiunto un controllo WPF al progetto, è possibile disporlo sul form.  
  
#### Per creare controlli WPF  
  
1.  Aggiungere un nuovo <xref:System.Windows.Controls.UserControl> WPF al progetto.  Usare il nome predefinito per il tipo di controllo, `UserControl1.xaml`.  Per altre informazioni, vedere [Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).  
  
2.  In visualizzazione Progettazione verificare che `UserControl1` sia selezionato.  Per altre informazioni, vedere [Procedura: selezionare e spostare elementi sull'area di progettazione](http://msdn.microsoft.com/it-it/54cb70b6-b35b-46e4-a0cc-65189399c474).  
  
3.  Nella finestra **Proprietà** impostare il valore delle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> su `200`.  
  
4.  Impostare il valore della proprietà <xref:System.Windows.Controls.Control.Background%2A> su `Blue`.  
  
5.  Compilare il progetto.  
  
## Hosting di controlli WPF in un pannello di layout  
 È possibile usare i controlli WPF nei pannelli di layout nello stesso modo in cui si usano gli altri controlli Windows Form.  
  
#### Per ospitare controlli WPF in un pannello di layout  
  
1.  Aprire `Form1` in Progettazione Windows Form.  
  
2.  Nella **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> nel form.  
  
3.  Nel pannello smart tag del controllo <xref:System.Windows.Forms.TableLayoutPanel> selezionare **Rimuovi ultima riga**.  
  
4.  Ridimensionare il controllo <xref:System.Windows.Forms.TableLayoutPanel> impostando una larghezza e un'altezza maggiori.  
  
5.  Nella **Casella degli strumenti** fare doppio clic su `UserControl1` per creare un'istanza di `UserControl1` nella prima cella del controllo<xref:System.Windows.Forms.TableLayoutPanel>.  
  
     L'istanza di `UserControl1` viene inclusa in un nuovo controllo <xref:System.Windows.Forms.Integration.ElementHost> denominato `elementHost1`.  
  
6.  Nella **Casella degli strumenti** fare doppio clic su `UserControl1` per creare un'altra istanza nella seconda cella del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
7.  Nella finestra **Struttura documento** selezionare `tableLayoutPanel1`.  Per altre informazioni, vedere [Document Outline Window](http://msdn.microsoft.com/it-it/9054f2bc-f6f8-4242-9fe0-be71089b12f8).  
  
8.  Nella finestra **Proprietà** impostare il valore della proprietà <xref:System.Windows.Forms.Control.Padding%2A> su `10, 10, 10, 10`.  
  
     Entrambi i controlli <xref:System.Windows.Forms.Integration.ElementHost> vengono ridimensionati per essere adattati al nuovo layout.  
  
## Allineamento dei controlli WPF mediante le guide di allineamento  
 Le guide di allineamento semplificano l'allineamento dei controlli su un form.  È possibile usare le guide di allineamento anche per allineare i controlli WPF.  Per altre informazioni, vedere [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md).  
  
#### Per usare le guide di allineamento per allineare i controlli WPF  
  
1.  Dalla **Casella degli strumenti** trascinare un'istanza di `UserControl1` sul form e posizionarla nello spazio sotto il controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
     L'istanza di `UserControl1` viene inclusa in un nuovo controllo <xref:System.Windows.Forms.Integration.ElementHost> denominato `elementHost3`.  
  
2.  Tramite le guide di allineamento allineare il bordo sinistro di `elementHost3` al bordo sinistro del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
3.  Tramite le guide di allineamento ridimensionare `elementHost3` impostando la stessa larghezza del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
4.  Spostare `elementHost3` verso il controllo <xref:System.Windows.Forms.TableLayoutPanel> finché non viene visualizzata una guida di allineamento centrale tra i due controlli.  
  
5.  Nella finestra **Proprietà** impostare il valore della proprietà Margin su `20, 20, 20, 20`.  
  
6.  Spostare `elementHost3` dal controllo <xref:System.Windows.Forms.TableLayoutPanel> finché non viene di nuovo visualizzata la guida di allineamento centrale.  La guida di allineamento centrale indica ora un margine di 20.  
  
7.  Spostare `elementHost3` verso destra fino ad allineare il bordo sinistro a quello di `elementHost1`.  
  
8.  Modificare la larghezza di `elementHost3` finché il bordo destro non è allineato a quello destro di `elementHost2`.  
  
## Ancoraggio e aggancio di controlli WPF  
 Un controllo WPF incluso in un form è soggetto alle stesse regole di ancoraggio e aggancio degli altri controlli Windows Form.  
  
#### Per ancorare e agganciare i controlli WPF  
  
1.  Selezionare `elementHost1`.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> su **Top, Bottom, Left, Right**.  
  
3.  Ridimensionare il controllo <xref:System.Windows.Forms.TableLayoutPanel> impostando dimensioni superiori.  
  
     Il controllo `elementHost1` verrà ridimensionato fino ad occupare l'intera cella.  
  
4.  Selezionare `elementHost2`.  
  
5.  Nella finestra **Proprietà** impostare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
     Il controllo `elementHost2` verrà ridimensionato fino ad occupare l'intera cella.  
  
6.  Selezionare il controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
7.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
8.  Selezionare `elementHost3`.  
  
9. Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
     Il controllo `elementHost3` verrà ridimensionato fino a occupare lo spazio rimanente sul form.  
  
10. Ridimensionare il form.  
  
     Tutti e tre i controlli <xref:System.Windows.Forms.Integration.ElementHost> verranno ridimensionati in maniera appropriata.  
  
     Per altre informazioni, vedere [Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [Procedura: allineare un controllo ai bordi dei form in fase di progettazione](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [Utilizzo di controlli WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)