---
title: "Procedura dettagliata: assegnazione del contenuto WPF in Windows Form in fase di progettazione | Microsoft Docs"
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
  - "controllo ElementHost, assegnazione di contenuti WPF in fase di progettazione"
  - "interoperabilità [WPF]"
  - "Windows Form, assegnazioni di contenuto"
  - "contenuto WPF [Windows Form], assegnazione in fase di progettazione"
  - "controllo utente WPF, hosting in Windows Form"
ms.assetid: b3e9ef93-7e0f-4a2f-8f1e-3437609a1eb7
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura dettagliata: assegnazione del contenuto WPF in Windows Form in fase di progettazione
Questa procedura dettagliata illustra come selezionare i tipi di controllo Windows Presentation Foundation \(WPF\) da visualizzare nel form.  È possibile selezionare qualsiasi tipo di controllo WPF incluso nel progetto.  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creare il progetto.  
  
-   Creare i tipi di controllo WPF.  
  
-   Selezionare i controlli WPF.  
  
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
  
-   Creare un nuovo progetto Windows Forms Application in Visual Basic o Visual C\# denominato `SelectingWpfContent`.  
  
## Creazione di tipi di controllo WPF  
 Dopo avere aggiunto i tipi di controllo WPF al progetto, è possibile includerli in controlli <xref:System.Windows.Forms.Integration.ElementHost> diversi.  
  
#### Per creare i tipi di controllo WPF  
  
1.  Aggiungere un nuovo progetto WPF <xref:System.Windows.Controls.UserControl> alla soluzione.  Usare il nome predefinito per il tipo di controllo, `UserControl1.xaml`.  Per altre informazioni, vedere [Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).  
  
2.  In visualizzazione Progettazione verificare che `UserControl1` sia selezionato.  Per altre informazioni, vedere [Procedura: selezionare e spostare elementi sull'area di progettazione](http://msdn.microsoft.com/it-it/54cb70b6-b35b-46e4-a0cc-65189399c474).  
  
3.  Nella finestra **Proprietà** impostare il valore delle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> su `200`.  
  
4.  Aggiungere un controllo <xref:System.Windows.Controls.TextBox?displayProperty=fullName> a <xref:System.Windows.Controls.UserControl> e impostare il valore della proprietà <xref:System.Windows.Controls.TextBox.Text%2A> su Hosted Content.  
  
5.  Aggiungere un secondo controllo WPF <xref:System.Windows.Controls.UserControl> al progetto.  Usare il nome predefinito per il tipo di controllo, `UserControl2.xaml`.  
  
6.  Nella finestra **Proprietà** impostare il valore delle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> su `200`.  
  
7.  Aggiungere un controllo <xref:System.Windows.Controls.TextBox?displayProperty=fullName> a <xref:System.Windows.Controls.UserControl> e impostare il valore della proprietà <xref:System.Windows.Controls.TextBox.Text%2A> su Hosted Content 2.  
  
 **Nota**: in generale, è opportuno ospitare contenuto WPF più sofisticato.  Il controllo <xref:System.Windows.Controls.TextBox?displayProperty=fullName> è qui usato a solo a titolo esemplificativo.  
  
1.  Compilare il progetto.  
  
## Selezione di controlli WPF  
 È possibile assegnare contenuto WPF diverso a un controllo <xref:System.Windows.Forms.Integration.ElementHost> che include già contenuto.  
  
#### Per selezionare i controlli WPF  
  
1.  Aprire `Form1` in Progettazione Windows Form.  
  
2.  Nella **Casella degli strumenti** fare doppio clic su `UserControl1` per creare un'istanza di `UserControl1` nel form.  
  
     L'istanza di `UserControl1` viene inclusa in un nuovo controllo <xref:System.Windows.Forms.Integration.ElementHost> denominato `elementHost1`.  
  
3.  Nel pannello smart tag per `elementHost1`, aprire l'elenco a discesa **Selezione contenuto ospitato**.  
  
4.  Dall'elenco a discesa selezionare **UserControl2**.  
  
     Il controllo `elementHost1` include ora un'istanza del tipo `UserControl2`.  
  
5.  Nella finestra **Proprietà** verificare che la proprietà <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> sia impostata su **UserControl2**.  
  
6.  Nella **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.Integration.ElementHost> dal gruppo **Interoperabilità WPF** nel form.  
  
     Il nome predefinito del nuovo controllo è `elementHost2`.  
  
7.  Nel pannello smart tag per `elementHost2`, aprire l'elenco a discesa **Selezione contenuto ospitato**.  
  
8.  Dall'elenco a discesa selezionare **UserControl1**.  
  
9. Il controllo `elementHost2` include ora un'istanza del tipo `UserControl1`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [Utilizzo di controlli WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)