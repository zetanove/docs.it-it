---
title: "Procedura: aggiungere la gestione di classi per un evento indirizzato | Microsoft Docs"
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
  - "gestori classi, eventi indirizzati"
  - "eventi indirizzati, gestori classi"
  - "task_core_add_class_handling_routed_event"
ms.assetid: 15b7b06c-9112-4ee5-b30a-65d10c5c5df6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: aggiungere la gestione di classi per un evento indirizzato
È possibile gestire gli eventi indirizzati mediante gestori di classi o gestori di istanze su qualsiasi nodo specificato nella route.  I gestori di classi vengono richiamati per primi e possono essere utilizzati dalle implementazioni di classi per sopprimere eventi dalla gestione di istanze o introdurre altri comportamenti specifici degli eventi su eventi di proprietà delle classi di base.  In questo esempio vengono illustrate due tecniche strettamente correlate per l'implementazione di gestori di classi.  
  
## Esempio  
 In questo esempio viene utilizzata una classe personalizzata basata sul pannello <xref:System.Windows.Controls.Canvas>.  L'applicazione si basa sulla premessa che la classe personalizzata introduce i comportamenti sugli elementi figlio, incluse le operazioni di intercettazione dei clic del pulsante sinistro del mouse e di contrassegno di tali eventi come gestiti, prima che la classe dell'elemento figlio o qualsiasi gestore di istanze su di essa vengano richiamati.  
  
 La classe <xref:System.Windows.UIElement> espone un metodo virtuale che abilita la gestione di classi sull'evento <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown>, con il semplice override dell'evento.  Si tratta della modalità più semplice per implementare la gestione di classi se tale metodo virtuale è disponibile nella gerarchia delle classi.  Nel codice seguente viene illustrata l'implementazione di <xref:System.Windows.UIElement.OnPreviewMouseLeftButtonDown%2A> in "MyEditContainer" derivato da <xref:System.Windows.Controls.Canvas>.  L'implementazione contrassegna l'evento come gestito negli argomenti, quindi aggiunge codice per apportare all'elemento di origine una modifica visibile di base.  
  
 [!code-csharp[ClassHandling#OnStarClassHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#onstarclasshandler)]
 [!code-vb[ClassHandling#OnStarClassHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#onstarclasshandler)]  
  
 Se nessun metodo virtuale è disponibile sulle classi di base o per il metodo specifico, la gestione di classi può essere aggiunta utilizzando direttamente un metodo di utilità di <xref:System.Windows.EventManager>, <xref:System.Windows.EventManager.RegisterClassHandler%2A>.  Questo metodo deve essere chiamato solo all'interno dell'inizializzazione statica delle classi che aggiungono la gestione di classi.  In questo esempio viene aggiunto un altro gestore per <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> e in questo caso la classe registrata è la classe personalizzata.  Al contrario, in caso di utilizzo di virtuali, la classe registrata è effettivamente la classe di base <xref:System.Windows.UIElement>.  Nei casi in cui la gestione di classi viene registrata dalle classi di base e dalla sottoclasse, i gestori della sottoclasse vengono richiamati per primi.  Il comportamento in un'applicazione comporterebbe innanzitutto la visualizzazione della finestra di messaggio di questo gestore, quindi la visualizzazione della modifica visiva nel gestore del metodo virtuale.  
  
 [!code-csharp[ClassHandling#StaticAndRegisterClassHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#staticandregisterclasshandler)]
 [!code-vb[ClassHandling#StaticAndRegisterClassHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#staticandregisterclasshandler)]  
  
## Vedere anche  
 <xref:System.Windows.EventManager>   
 [Contrassegno degli eventi indirizzati come gestiti e gestione delle classi](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)   
 [Gestire un evento indirizzato](../../../../docs/framework/wpf/advanced/how-to-handle-a-routed-event.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)