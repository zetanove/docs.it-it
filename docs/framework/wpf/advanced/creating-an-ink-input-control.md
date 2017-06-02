---
title: "Creazione di un controllo di input penna | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "raccolta di tratti input penna"
  - "DynamicRenderer (oggetti)"
  - "input penna (controllo)"
  - "tratti input penna, raccolta"
  - "tratti input penna, gestione"
  - "input penna, rendering"
  - "input dal mouse, accettazione"
  - "gestione di tratti input penna"
  - "input del mouse, accettazione"
  - "rendering di input penna"
  - "StylusPlugIn (oggetti)"
ms.assetid: c31f3a67-cb3f-4ded-af9e-ed21f6575b26
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Creazione di un controllo di input penna
È possibile creare un controllo personalizzato per eseguire il rendering dinamico e statico dell'input penna,  ovvero per eseguire il rendering dell'input penna mentre un utente traccia un tratto, in modo che l'input sembri "fluire" dalla penna del Tablet PC, e quindi visualizzarlo dopo che è stato aggiunto al controllo, tramite la penna del Tablet PC oppure incollandolo dagli Appunti o caricandolo da un file.  Per eseguire il rendering dinamico dell'input penna, è necessario che il controllo utilizzi un oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>.  Per eseguire il rendering statico dell'input penna, è necessario eseguire l'override dei metodi degli eventi dello stilo \(<xref:System.Windows.UIElement.OnStylusDown%2A>, <xref:System.Windows.UIElement.OnStylusMove%2A> e <xref:System.Windows.UIElement.OnStylusUp%2A>\) per raccogliere i dati <xref:System.Windows.Input.StylusPoint>, creare tratti e aggiungerli a un oggetto <xref:System.Windows.Controls.InkPresenter>, che esegue il rendering dell'input penna sul controllo.  
  
 In questo argomento sono contenute le seguenti sottosezioni:  
  
-   [Procedura: raccogliere dati dei punti dello stilo e creare tratti input penna](#CollectingStylusPointDataAndCreatingInkStrokes)  
  
-   [Procedura: abilitare il controllo per l'accettazione di input dal mouse](#EnablingYourControlToAcceptInputTromTheMouse)  
  
-   [Esempio completo](#PuttingItTogether)  
  
-   [Utilizzo di plug-in aggiuntivi e oggetti DynamicRenderer](#UsingAdditionalPluginsAndDynamicRenderers)  
  
-   [Conclusione](#AdvancedInkHandling_Conclusion)  
  
<a name="CollectingStylusPointDataAndCreatingInkStrokes"></a>   
## Procedura: raccogliere dati dei punti dello stilo e creare tratti input penna  
 Per creare un controllo che raccolga e gestisca tratti input penna, effettuare le operazioni seguenti:  
  
1.  Derivare una classe da <xref:System.Windows.Controls.Control> o da una delle classi derivate da <xref:System.Windows.Controls.Control>, ad esempio <xref:System.Windows.Controls.Label>.  
  
     [!code-csharp[AdvancedInkTopicsSamples#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
    [!code-csharp[AdvancedInkTopicsSamples#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#14)]  
    [!code-csharp[AdvancedInkTopicsSamples#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#15)]  
  
2.  Aggiungere un oggetto <xref:System.Windows.Controls.InkPresenter> alla classe e impostare la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> sul nuovo oggetto <xref:System.Windows.Controls.InkPresenter>.  
  
     [!code-csharp[AdvancedInkTopicsSamples#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#16)]  
  
3.  Collegare la proprietà <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> dell'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> all'oggetto <xref:System.Windows.Controls.InkPresenter> effettuando una chiamata al metodo <xref:System.Windows.Controls.InkPresenter.AttachVisuals%2A> e aggiungere l'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> alla raccolta <xref:System.Windows.UIElement.StylusPlugIns%2A>.  In questo modo l'oggetto <xref:System.Windows.Controls.InkPresenter> visualizza l'input penna via via che i punti dei dati dello stilo vengono raccolti dal controllo.  
  
     [!code-csharp[AdvancedInkTopicsSamples#17](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#17)]  
    [!code-csharp[AdvancedInkTopicsSamples#18](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#18)]  
  
4.  Eseguire l'override del metodo <xref:System.Windows.UIElement.OnStylusDown%2A>.  In questo metodo acquisire lo stilo con una chiamata a <xref:System.Windows.Input.Stylus.Capture%2A>.  Acquisendo lo stilo, il controllo continuerà a ricevere gli eventi <xref:System.Windows.UIElement.StylusMove> e <xref:System.Windows.UIElement.StylusUp>, anche se lo stilo lascia i limiti del controllo.  Questa operazione non è obbligatoria, ma è consigliabile nella maggior parte dei casi per migliorare l'esperienza dell'utente.  Creare un nuovo oggetto <xref:System.Windows.Input.StylusPointCollection> per raccogliere i dati <xref:System.Windows.Input.StylusPoint>.  Infine, aggiungere l'insieme iniziale dei dati <xref:System.Windows.Input.StylusPoint> all'oggetto <xref:System.Windows.Input.StylusPointCollection>.  
  
     [!code-csharp[AdvancedInkTopicsSamples#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#7)]  
  
5.  Eseguire l'override del metodo <xref:System.Windows.UIElement.OnStylusMove%2A> e aggiungere i dati <xref:System.Windows.Input.StylusPoint> all'oggetto <xref:System.Windows.Input.StylusPointCollection> creato in precedenza.  
  
     [!code-csharp[AdvancedInkTopicsSamples#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#8)]  
  
6.  Eseguire l'override del metodo <xref:System.Windows.UIElement.OnStylusUp%2A> e creare un nuovo oggetto <xref:System.Windows.Ink.Stroke> con i dati <xref:System.Windows.Input.StylusPointCollection>.  Aggiungere il nuovo oggetto <xref:System.Windows.Ink.Stroke> creato alla raccolta <xref:System.Windows.Controls.InkPresenter.Strokes%2A> dell'oggetto <xref:System.Windows.Controls.InkPresenter> e rilasciare l'acquisizione dello stilo.  
  
     [!code-csharp[AdvancedInkTopicsSamples#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#10)]  
  
<a name="EnablingYourControlToAcceptInputTromTheMouse"></a>   
## Procedura: abilitare il controllo per l'accettazione di input dal mouse  
 Se si aggiunge all'applicazione e si esegue il controllo precedente, quindi si utilizza il mouse come dispositivo di input, si noterà che i tratti non vengono mantenuti.  Per mantenere i tratti quando si utilizza il mouse come dispositivo di input, effettuare le operazioni seguenti:  
  
1.  Eseguire l'override del metodo <xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A> e creare un nuovo oggetto <xref:System.Windows.Input.StylusPointCollection>. Ottenere la posizione del mouse quando si è verificato l'evento e creare un oggetto <xref:System.Windows.Input.StylusPoint> utilizzando i dati dei punti, quindi aggiungere l'oggetto <xref:System.Windows.Input.StylusPoint> all'oggetto <xref:System.Windows.Input.StylusPointCollection>.  
  
     [!code-csharp[AdvancedInkTopicsSamples#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#11)]  
  
2.  Eseguire l'override del metodo <xref:System.Windows.UIElement.OnMouseMove%2A>.  Ottenere la posizione del mouse quando si è verificato l'evento e creare un oggetto <xref:System.Windows.Input.StylusPoint> utilizzando i dati dei punti.  Aggiungere l'oggetto <xref:System.Windows.Input.StylusPoint> all'oggetto <xref:System.Windows.Input.StylusPointCollection> creato in precedenza.  
  
     [!code-csharp[AdvancedInkTopicsSamples#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#12)]  
  
3.  Eseguire l'override del metodo <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A>.  Creare un nuovo oggetto <xref:System.Windows.Ink.Stroke> con i dati <xref:System.Windows.Input.StylusPointCollection> e aggiungere il nuovo oggetto <xref:System.Windows.Ink.Stroke> creato alla raccolta <xref:System.Windows.Controls.InkPresenter.Strokes%2A> dell'oggetto <xref:System.Windows.Controls.InkPresenter>.  
  
     [!code-csharp[AdvancedInkTopicsSamples#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#13)]  
  
<a name="PuttingItTogether"></a>   
## Esempio completo  
 Nell'esempio seguente viene illustrato un controllo personalizzato che raccoglie l'input penna quando l'utente utilizza il mouse o la penna.  
  
 [!code-csharp[AdvancedInkTopicsSamples#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
[!code-csharp[AdvancedInkTopicsSamples#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#6)]  
  
<a name="UsingAdditionalPluginsAndDynamicRenderers"></a>   
## Utilizzo di plug\-in aggiuntivi e oggetti DynamicRenderer  
 Analogamente agli InkCanvas, il controllo personalizzato può includere un oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> personalizzato e oggetti <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> aggiuntivi.  Aggiungere questi oggetti alla raccolta <xref:System.Windows.UIElement.StylusPlugIns%2A>.  L'ordine degli oggetti <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> nell'insieme <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> influisce sull'aspetto dell'input penna quando viene sottoposto a rendering.  Si supponga di disporre di un oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> denominato `dynamicRenderer` e di un oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> personalizzato denominato `translatePlugin` che esegue l'offset dell'input della penna del Tablet PC.  Se `translatePlugin` è il primo oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> nell'insieme <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> e `dynamicRenderer` è il secondo, l'input penna che "fluisce" verrà sottoposto a offset mentre l'utente sposta la penna.  Se `dynamicRenderer` è il primo e `translatePlugin` è il secondo oggetto, l'input penna verrà sottoposto a offset solo quando l'utente solleva la penna.  
  
<a name="AdvancedInkHandling_Conclusion"></a>   
## Conclusione  
 È possibile creare un controllo che raccoglie l'input penna e lo sottopone a rendering eseguendo l'override dei metodi degli eventi dello stilo.  Creando un controllo personalizzato, derivando le classi <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> e inserendole nell'insieme <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>, è possibile implementare di fatto qualsiasi comportamento immaginabile con l'input penna.  Ottenendo l'accesso ai dati <xref:System.Windows.Input.StylusPoint> mentre vengono generati, è possibile personalizzare l'input di <xref:System.Windows.Input.Stylus> e sottoporlo a rendering sullo schermo nel modo appropriato per l'applicazione.  Grazie all'accesso di basso livello ai dati <xref:System.Windows.Input.StylusPoint>, è possibile implementare la raccolta e il rendering dell'input penna con prestazioni ottimali per l'applicazione.  
  
## Vedere anche  
 [Gestione avanzata dell'input penna](../../../../docs/framework/wpf/advanced/advanced-ink-handling.md)   
 [Accesso e modifica dell'input penna](http://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)