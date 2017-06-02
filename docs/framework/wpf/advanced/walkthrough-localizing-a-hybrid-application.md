---
title: "Procedura dettagliata: localizzazione di un&#39;applicazione ibrida | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "applicazioni ibride [interoperabilità WPF]"
  - "localizzazione [interoperabilità WPF]"
ms.assetid: fbc0c54e-930a-4c13-8e9c-27b83665010a
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura dettagliata: localizzazione di un&#39;applicazione ibrida
In questa procedura dettagliata viene illustrato come localizzare elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in un'applicazione ibrida basata su [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione del progetto host [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
-   Aggiunta di contenuto localizzabile.  
  
-   Abilitazione della localizzazione  
  
-   Assegnazione di identificatori di risorsa  
  
-   Utilizzo dello strumento LocBaml per produrre un assembly satellite.  
  
 Per un elenco di codice completo delle attività illustrate in questa procedura dettagliata, vedere [Esempio di localizzazione di un'applicazione ibrida](http://go.microsoft.com/fwlink/?LinkID=160015) \(la pagina potrebbe essere in inglese\).  
  
 Al termine, sarà disponibile un'applicazione ibrida localizzata.  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
## Creazione del progetto host Windows Form  
 Il primo passaggio consiste nella creazione del progetto dell'applicazione [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e nell'aggiunta di un elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] con contenuto da localizzare.  
  
#### Per creare il progetto host  
  
1.  Creare un progetto di applicazione WPF denominato `LocalizingWpfInWf`.  Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Aggiungere un elemento <xref:System.Windows.Controls.UserControl> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] denominato `SimpleControl` al progetto.  
  
3.  Utilizzare il controllo <xref:System.Windows.Forms.Integration.ElementHost> per posizionare un elemento `SimpleControl` del form.  Per ulteriori informazioni, vedere [Procedura dettagliata: hosting di controlli compositi 3D di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md).  
  
## Aggiunta di contenuto localizzabile  
 Verrà in seguito aggiunto un controllo etichetta [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e impostato il contenuto dell'elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] su una stringa localizzabile.  
  
#### Per aggiungere contenuto localizzabile  
  
1.  In Esplora soluzioni fare doppio clic su **SimpleControl.xaml** per aprirlo in [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
2.  Impostare il contenuto del controllo <xref:System.Windows.Controls.Button> utilizzando il codice riportato di seguito.  
  
     [!code-xml[LocalizingWpfInWf#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl0.xaml#10)]  
  
3.  In Esplora soluzioni fare doppio clic su **Form1** per aprirlo in Progettazione Windows Form.  
  
4.  Aprire la Casella degli strumenti e fare doppio clic su **Etichetta** per aggiungere un controllo etichetta al form.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Text%2A> su `"Hello"`.  
  
5.  Premere F5 per compilare ed eseguire l'applicazione.  
  
     Sia sull'elemento `SimpleControl` sia sul controllo etichetta verrà visualizzato il testo **"Hello"**.  
  
## Abilitazione della localizzazione  
 La finestra Progettazione Windows Form fornisce le impostazioni per abilitare la localizzazione in un assembly satellite.  
  
#### Per abilitare la localizzazione  
  
1.  In Esplora soluzioni fare doppio clic su **Form1.cs** per aprirlo in Progettazione Windows Form.  
  
2.  Nella finestra Proprietà impostare il valore della proprietà **Localizable** del form su `true`.  
  
3.  Nella finestra Proprietà impostare il valore della proprietà **Language** su **Spagnolo \(Spagna\)**.  
  
4.  In Progettazione Windows Form selezionare il controllo etichetta.  
  
5.  Nella finestra Proprietà impostare il valore della proprietà <xref:System.Windows.Forms.Control.Text%2A> su `"Hola"`.  
  
     Un nuovo file di risorse denominato Form1.es\-ES.resx verrà aggiunto al progetto.  
  
6.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Form1.cs**, quindi scegliere **Visualizza codice** per aprirlo nell'editor di codice.  
  
7.  Copiare il seguente codice nel costruttore `Form1`, prima di chiamare `InitializeComponent`.  
  
     [!code-csharp[LocalizingWpfInWf#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/Form1.cs#2)]  
  
8.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **LocalizingWpfInWf**, quindi scegliere **Scarica progetto**.  
  
     Al progetto viene assegnata l'etichetta **\(non disponibile\)**.  
  
9. Fare clic con il pulsante destro del mouse su **LocalizingWpfInWf**, quindi scegliere **Modifica LocalizingWpfInWf.csproj**.  
  
     Il file di progetto verrà aperto nell'editor di codice.  
  
10. Copiare il la riga riportata di seguito nel primo elemento `PropertyGroup` nel file di progetto.  
  
    ```  
    <UICulture>en-US</UICulture>   
    ```  
  
11. Salvare e chiudere il file di progetto.  
  
12. In Esplora soluzioni fare clic con il pulsante destro del mouse su **LocalizingWpfInWf**, quindi scegliere **Ricarica progetto**.  
  
## Assegnazione di identificatori di risorsa  
 È possibile eseguire il mapping del contenuto localizzabile alle assembly di risorse utilizzando identificatori di risorsa.  L'applicazione MsBuild.exe assegna automaticamente identificatori di risorsa quando si specifica l'opzione `updateuid`.  
  
#### Per assegnare identificatori di risorsa  
  
1.  Dal menu Start aprire il prompt dei comandi [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
2.  Per assegnare identificatori di risorsa al contenuto localizzabile, utilizzare il comando seguente.  
  
    ```  
    msbuild /t:updateuid LocalizingWpfInWf.csproj  
    ```  
  
3.  In Esplora soluzioni fare doppio clic su **SimpleControl.xaml** per aprirlo nell'editor del codice.  Sarà visualizzato il comando `msbuild` che ha aggiunto l'attributo `Uid` a tutti gli elementi.  In tal modo si semplifica la localizzazione mediante l'assegnazione di identificatori di risorsa.  
  
     [!code-xml[LocalizingWpfInWf#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl.xaml#20)]  
  
4.  Premere F6 per compilare la soluzione.  
  
## Utilizzo dello strumento LocBaml per produrre un assembly satellite.  
 Il contenuto localizzato viene memorizzato in un *assembly satellite* di sole risorse  Utilizzare lo strumento della riga di comando LocBaml.exe per produrre un assembly localizzato per il contenuto[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
#### Per produrre un assembly satellite  
  
1.  Copiare lo strumento LocBaml.exe nella cartelle obj\\Debug del progetto.  Per ulteriori informazioni, vedere [Localizzare un'applicazione](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md).  
  
2.  Nella finestra del prompt dei comandi utilizzare il comando seguente per estrarre stringhe di risorsa in un file temporaneo.  
  
    ```  
    LocBaml /parse LocalizingWpfInWf.g.en-US.resources /out:temp.csv  
    ```  
  
3.  Aprire il file temp.csv con [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] o con un altro editor di testo.  Sostituire la stringa `"Hello"` con la relativa traduzione spagnola, `"Hola"`.  
  
4.  Salvare il file temp.csv.  
  
5.  Per generare il file di risorse localizzato, utilizzare il comando seguente.  
  
    ```  
    LocBaml /generate /trans:temp.csv LocalizingWpfInWf.g.en-US.resources /out:. /cul:es-ES  
    ```  
  
     Il file di risorse LocalizingWpfInWf.g.es\-ES. viene creato nella cartella obj\\Debug.  
  
6.  Per compilare l'assembly satellite localizzato, utilizzare il seguente comando.  
  
    ```  
    Al.exe /out:LocalizingWpfInWf.resources.dll /culture:es-ES /embed:LocalizingWpfInWf.Form1.es-ES.resources /embed:LocalizingWpfInWf.g.es-ES.resources  
    ```  
  
     Il file LocalizingWpfInWf.resources.dll viene creato nella cartella obj\\Debug.  
  
7.  Copiare il file LocalizingWpfInWf.resources.dll nella cartella bin\\Debug\\es\-ES del progetto..  Sostituire il file esistente.  
  
8.  Eseguire LocalizingWpfInWf.exe, situato nella cartella bin\\Debug folder del progetto.  Non ricompilare l'applicazione oppure l'assembly satellite verrà sovrascritto.  
  
     Nell'applicazione vengono visualizzate le stringhe localizzate invece delle stringhe in inglese.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Localizzare un'applicazione](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)   
 [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/it-it/9a96220d-a19b-4de0-9f48-01e5d82679e5)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)