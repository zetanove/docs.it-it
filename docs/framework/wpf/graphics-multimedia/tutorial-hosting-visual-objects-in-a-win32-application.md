---
title: "Esercitazione: hosting di oggetti visivi in un&#39;applicazione Win32 | Microsoft Docs"
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
  - "hosting, oggetti Visual in codice Win32"
  - "oggetti Visual in codice Win32"
  - "codice Win32, oggetti Visual"
ms.assetid: f0e1600c-3217-43d5-875d-1864fa7fe628
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Esercitazione: hosting di oggetti visivi in un&#39;applicazione Win32
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce un ambiente dettagliato per la creazione di applicazioni.  Tuttavia, se si utilizza una grande quantità di codice [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)], può essere più efficace aggiungere funzionalità [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] all'applicazione anziché riscrivere il codice.  Per fornire un supporto per i sottosistemi grafici di [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] e di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizzati contemporaneamente in un'applicazione, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce un meccanismo per ospitare oggetti in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
 In questa esercitazione viene illustrato come scrivere un'applicazione di esempio, disponibile in [Esempio di hit test con interoperatività Win32](http://go.microsoft.com/fwlink/?LinkID=159995) \(la pagina potrebbe essere in inglese\), che ospita oggetti visivi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
   
  
<a name="requirements"></a>   
## Requisiti  
 Per questa esercitazione si presuppone una conoscenza di base della programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Per un'introduzione alla programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md).  Per un'introduzione alla programmazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], vedere uno qualsiasi dei numerosi manuali sull'argomento, in particolare *Programmare Windows* di Charles Petzold.  
  
> [!NOTE]
>  In questa esercitazione sono inclusi diversi esempi di codice relativi all'esempio associato.  Tuttavia, per una questione di leggibilità, il codice di esempio completo non è compreso.  Per il codice di esempio completo, vedere [Esempio di hit test con interoperatività Win32](http://go.microsoft.com/fwlink/?LinkID=159995).  
  
<a name="creating_the_host_win32_window"></a>   
## Creazione di una finestra Win32 host  
 La chiave per ospitare oggetti [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] è la classe <xref:System.Windows.Interop.HwndSource>.  Questa classe esegue il wrapping degli oggetti [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], consentendo di incorporarli nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] come finestra figlio.  
  
 Nell'esempio seguente viene mostrato il codice per la creazione dell'oggetto <xref:System.Windows.Interop.HwndSource> come finestra contenitore [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] per gli oggetti visivi.  Per impostare lo stile, la posizione e altri parametri della finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], utilizzare l'oggetto <xref:System.Windows.Interop.HwndSourceParameters>.  
  
 [!code-csharp[VisualsHitTesting#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#101)]
 [!code-vb[VisualsHitTesting#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#101)]  
  
> [!NOTE]
>  Il valore della proprietà <xref:System.Windows.Interop.HwndSourceParameters.ExtendedWindowStyle%2A> non può essere impostato su WS\_EX\_TRANSPARENT.  Di conseguenza, la finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host non può essere trasparente  e per questo motivo il colore di sfondo della finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host sarà impostato sullo stesso colore di sfondo della finestra padre.  
  
<a name="adding_visual_objects_to_the_host_win32_window"></a>   
## Aggiunta di oggetti visivi alla finestra Win32 host  
 Una volta creata una finestra contenitore [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host per gli oggetti visivi, è possibile aggiungere tali oggetti alla finestra.  Sarà necessario che qualsiasi trasformazione degli oggetti visivi, ad esempio le animazioni, non si estendano oltre i limiti del rettangolo di delimitazione della finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host.  
  
 Nell'esempio seguente viene mostrato il codice per la creazione dell'oggetto <xref:System.Windows.Interop.HwndSource> e l'aggiunta di oggetti visivi a tale oggetto.  
  
> [!NOTE]
>  La proprietà <xref:System.Windows.Interop.HwndSource.RootVisual%2A> dell'oggetto <xref:System.Windows.Interop.HwndSource> è impostata sul primo oggetto visivo aggiunto alla finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host.  L'oggetto visivo radice definisce il nodo di primo livello della struttura ad albero di oggetti visivi.  Eventuali oggetti visivi aggiunti successivamente alla finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host vengono inseriti come oggetti figlio.  
  
 [!code-csharp[VisualsHitTesting#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#100)]
 [!code-vb[VisualsHitTesting#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#100)]  
  
<a name="implementing_the_win32_message_filter"></a>   
## Implementazione del filtro messaggi Win32  
 La finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host per gli oggetti visivi richiede una procedura del filtro messaggi della finestra per gestire i messaggi inviati alla finestra dalla coda dell'applicazione.  La routine della finestra riceve i messaggi dal sistema [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Può trattarsi di messaggi di input o di messaggi di gestione della finestra.  È possibile facoltativamente gestire un messaggio nella routine della finestra oppure passarlo al sistema per l'elaborazione predefinita.  
  
 L'oggetto <xref:System.Windows.Interop.HwndSource> definito come elemento padre per gli oggetti visivi deve fare riferimento alla routine del filtro messaggi della finestra fornita.  Al momento della creazione dell'oggetto <xref:System.Windows.Interop.HwndSource>, impostare la proprietà <xref:System.Windows.Interop.HwndSourceParameters.HwndSourceHook%2A> in modo da fare riferimento alla routine della finestra.  
  
 [!code-csharp[VisualsHitTesting#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#102)]
 [!code-vb[VisualsHitTesting#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#102)]  
  
 Nell'esempio seguente viene mostrato il codice per la gestione dei messaggi di rilascio dei pulsanti sinistro e destro del mouse.  Il valore di coordinate della posizione rilevata del mouse è contenuto nel valore del parametro `lParam`.  
  
 [!code-csharp[VisualsHitTesting#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
<a name="processing_the_win32_messages"></a>   
## Elaborazione dei messaggi Win32  
 Nel codice dell'esempio seguente viene illustrata l'esecuzione di un hit test sulla gerarchia di oggetti visivi contenuta nella finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host.  È possibile individuare se un punto è compreso all'interno della geometria di un oggetto visivo utilizzando il metodo <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> per specificare l'oggetto visivo radice e il valore delle coordinate in base a cui eseguire l'hit test.  In questo caso, l'oggetto visivo radice è il valore della proprietà <xref:System.Windows.Interop.HwndSource.RootVisual%2A> dell'oggetto <xref:System.Windows.Interop.HwndSource>.  
  
 [!code-csharp[VisualsHitTesting#104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 Per ulteriori informazioni sull'hit testing su oggetti visivi, vedere [Hit testing a livello visivo](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md).  
  
## Vedere anche  
 <xref:System.Windows.Interop.HwndSource>   
 [Esempio di hit test con interoperatività Win32](http://go.microsoft.com/fwlink/?LinkID=159995)   
 [Hit testing a livello visivo](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)