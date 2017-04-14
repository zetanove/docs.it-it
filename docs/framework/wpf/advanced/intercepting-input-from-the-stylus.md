---
title: "Intercettazione dell&#39;input dello stilo | Microsoft Docs"
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
  - "architettura, System.Windows.Input.StylusPlugIns"
  - "InkCanvas, aggiunta di plug-in"
  - "plug-in, stilo"
  - "StylusPlugIns (architettura)"
  - "System.Windows.Input.StylusPlugIns (architettura)"
ms.assetid: 791bb2f0-4e5c-4569-ac3c-211996808d44
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Intercettazione dell&#39;input dello stilo
L'architettura <xref:System.Windows.Input.StylusPlugIns> fornisce un meccanismo per l'implementazione del controllo di basso livello sull'input di <xref:System.Windows.Input.Stylus> e la creazione di oggetti <xref:System.Windows.Ink.Stroke> di input penna.  La classe <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> fornisce un meccanismo per implementare il comportamento personalizzato e applicarlo al flusso di dati provenienti dal dispositivo stilo per prestazioni ottimali.  
  
 In questo argomento sono contenute le seguenti sottosezioni:  
  
-   [Architettura](#Architecture)  
  
-   [Implementazione dei plug-in dello stilo](#ImplementingStylusPlugins)  
  
-   [Aggiunta del plug-in a un InkCanvas](#AddingYourPluginToAnInkCanvas)  
  
-   [Conclusione](#Conclusion)  
  
<a name="Architecture"></a>   
## Architettura  
 La classe <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> rappresenta l'evoluzione delle API [StylusInput](http://go.microsoft.com/fwlink/?LinkId=50753&clcid=0x409), descritte nel documento [Accesso e modifica dell'input penna](http://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409), in [Microsoft Windows XP Tablet PC Edition Software Development Kit 1.7](http://go.microsoft.com/fwlink/?linkid=11782&clcid=0x409)  
  
 Ogni oggetto <xref:System.Windows.UIElement> include una proprietà <xref:System.Windows.UIElement.StylusPlugIns%2A> che corrisponde a un oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>.  È possibile aggiungere un oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> alla proprietà <xref:System.Windows.UIElement.StylusPlugIns%2A> di un elemento per modificare i dati di <xref:System.Windows.Input.StylusPoint> al momento della generazione.  I dati di <xref:System.Windows.Input.StylusPoint> sono costituiti da tutte le proprietà supportate dal digitalizzatore del sistema, inclusi i dati dei punti <xref:System.Windows.Input.StylusPoint.X%2A> e <xref:System.Windows.Input.StylusPoint.Y%2A> e i dati <xref:System.Windows.Input.StylusPoint.PressureFactor%2A>.  
  
 Gli oggetti <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> vengono inseriti direttamente nel flusso di dati provenienti dal dispositivo <xref:System.Windows.Input.Stylus> quando si aggiunge l'oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> alla proprietà <xref:System.Windows.UIElement.StylusPlugIns%2A>.  L'ordine in cui i plug\-in vengono aggiunti alla raccolta <xref:System.Windows.UIElement.StylusPlugIns%2A> definisce l'ordine in cui riceveranno i dati <xref:System.Windows.Input.StylusPoint>.  Ad esempio, se si aggiunge un plug\-in di filtro che restringe l'input ad una particolare area e quindi si aggiunge un plug\-in che riconosce i movimenti quando vengono scritti, tale plug\-in riceverà dati <xref:System.Windows.Input.StylusPoint> filtrati.  
  
<a name="ImplementingStylusPlugins"></a>   
## Implementazione dei plug\-in dello stilo  
 Per implementare un plug\-in, derivare una classe da <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>.  Questa classe viene applicata al flusso di dati provenienti dall'oggetto <xref:System.Windows.Input.Stylus>.  In questa classe è possibile modificare i valori dei dati <xref:System.Windows.Input.StylusPoint>.  
  
> [!CAUTION]
>  Se una classe <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> genera o causa un'eccezione, l'applicazione verrà chiusa.  È necessario svolgere test accurati sui controlli che utilizzano un oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> e utilizzare un controllo solo se si è certi che l'oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> non genererà un'eccezione.  
  
 Nell'esempio seguente viene illustrato un plug\-in che restringe l'input dello stilo modificando i valori <xref:System.Windows.Input.StylusPoint.X%2A> e <xref:System.Windows.Input.StylusPoint.Y%2A> nei dati <xref:System.Windows.Input.StylusPoint> provenienti dal dispositivo <xref:System.Windows.Input.Stylus>.  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#3)]
[!code-vb[AdvancedInkTopicsSamples#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#3)]  
  
<a name="AddingYourPluginToAnInkCanvas"></a>   
## Aggiunta del plug\-in a un InkCanvas  
 Il modo più semplice per utilizzare il plug\-in personalizzato consiste nell'implementare una classe che deriva da InkCanvas e aggiungerla alla proprietà <xref:System.Windows.UIElement.StylusPlugIns%2A>.  
  
 Nell'esempio seguente viene illustrato un oggetto <xref:System.Windows.Controls.InkCanvas> personalizzato che filtra l'input penna.  
  
 [!code-csharp[AdvancedInkTopicsSamples#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#4)]  
  
 Se si aggiunge un oggetto `FilterInkCanvas` all'applicazione e la si esegue, si noterà che l'input penna viene limitato a un'area solo dopo che l'utente completa un tratto.  Ciò è dovuto al fatto che l'oggetto <xref:System.Windows.Controls.InkCanvas> include una proprietà <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> che corrisponde a un oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> ed è già un membro della raccolta <xref:System.Windows.UIElement.StylusPlugIns%2A>.  L'oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> personalizzato aggiunto alla raccolta <xref:System.Windows.UIElement.StylusPlugIns%2A> riceve i dati <xref:System.Windows.Input.StylusPoint> dopo che <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> riceve dati.  Di conseguenza, i dati <xref:System.Windows.Input.StylusPoint> verranno filtrati solo dopo che l'utente solleva la penna per terminare un tratto.  Per filtrare l'input penna via via che viene tracciato dall'utente, è necessario inserire l'oggetto `FilterPlugin` prima dell'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>.  
  
 Nel codice C\# seguente viene illustrato un oggetto <xref:System.Windows.Controls.InkCanvas> personalizzato che filtra l'input penna via via che viene tracciato.  
  
 [!code-csharp[AdvancedInkTopicsSamples#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#5)]  
  
<a name="Conclusion"></a>   
## Conclusione  
 Derivando le classi <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> e inserendole nelle raccolte <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>, è possibile migliorare notevolmente il comportamento dell'input penna.  Ottenendo l'accesso ai dati <xref:System.Windows.Input.StylusPoint> mentre vengono generati, è possibile personalizzare l'input <xref:System.Windows.Input.Stylus>.  Grazie all'accesso di basso livello ai dati <xref:System.Windows.Input.StylusPoint>, è possibile implementare la raccolta e il rendering dell'input penna con prestazioni ottimali per l'applicazione.  
  
## Vedere anche  
 [Gestione avanzata dell'input penna](../../../../docs/framework/wpf/advanced/advanced-ink-handling.md)   
 [Accesso e modifica dell'input penna](http://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)