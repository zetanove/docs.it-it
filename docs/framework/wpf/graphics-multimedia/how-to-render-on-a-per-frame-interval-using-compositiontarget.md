---
title: "Procedura: eseguire il rendering in un intervallo per frame tramite CompositionTarget | Microsoft Docs"
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
  - "CompositionTarget (oggetti), rendering per fotogramma"
  - "rendering per fotogramma tramite oggetti CompositionTarget"
ms.assetid: 701246cd-66b7-4d69-ada9-17b3b433d95d
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eseguire il rendering in un intervallo per frame tramite CompositionTarget
Il motore di animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce molte funzionalità per la creazione di animazioni basate su frame.  Tuttavia, esistono sono scenari di applicazioni in cui è necessario un controllo più specifico sul rendering per singolo frame.  L'oggetto <xref:System.Windows.Media.CompositionTarget> consente di creare animazioni personalizzate basate su un callback per frame.  
  
 <xref:System.Windows.Media.CompositionTarget> è una classe statica che rappresenta l'area di visualizzazione sulla quale viene disegnata l'applicazione.  L'evento <xref:System.Windows.Media.CompositionTarget.Rendering> viene generato ogni volta che viene disegnata la scena dell'applicazione.  La frequenza dei fotogrammi del rendering è il numero di volte al secondo in cui la scena viene disegnata.  
  
> [!NOTE]
>  Per un esempio di codice completo, in cui viene utilizzato <xref:System.Windows.Media.CompositionTarget>, vedere [Esempio dell'utilizzo di CompositionTarget](http://go.microsoft.com/fwlink/?LinkID=160045) \(la pagina potrebbe essere in inglese\).  
  
## Esempio  
 L'evento <xref:System.Windows.Media.CompositionTarget.Rendering> viene generato durante il processo di rendering di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Nell'esempio seguente viene illustrato come registrare un delegato <xref:System.EventHandler> per il metodo <xref:System.Windows.Media.CompositionTarget.Rendering> statico nell'oggetto <xref:System.Windows.Media.CompositionTarget>.  
  
 [!code-csharp[CompositionTargetSample#CompositionTarget1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CompositionTargetSample/CSharp/Window1.xaml.cs#compositiontarget1)]
 [!code-vb[CompositionTargetSample#CompositionTarget1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CompositionTargetSample/visualbasic/window1.xaml.vb#compositiontarget1)]  
  
 È possibile utilizzare il metodo per la gestione eventi di rendering per creare contenuto del disegno personalizzato.  Questo metodo per la gestione eventi viene chiamato una volta per ciascun frame.  Ogni volta che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esegue il marshalling dei dati di rendering permanenti della [struttura ad albero visuale](GTMT) nel grafico della scena della composizione, viene chiamato il metodo per la gestione eventi.  Inoltre, il metodo per la gestione eventi viene chiamato anche se le modifiche alla [struttura ad albero visuale](GTMT) forzano gli aggiornamenti al grafico della scena della composizione.  Notare che il metodo per la gestione eventi viene chiamato dopo che il layout è stato calcolato.  Tuttavia, è possibile modificare il layout nel metodo per la gestione eventi; in tal caso il layout verrà calcolato nuovamente prima di eseguire il rendering.  
  
 Nell'esempio seguente viene illustrato come è possibile fornire un disegno personalizzato in un metodo per la gestione eventi <xref:System.Windows.Media.CompositionTarget>.  In questo caso, il colore di sfondo dell'oggetto <xref:System.Windows.Controls.Canvas> viene disegnato con un valore di colore basato sulla posizione della coordinata del mouse.  Se si sposta il mouse all'interno dell'oggetto <xref:System.Windows.Controls.Canvas>, il relativo colore di sfondo cambia.  Inoltre, viene calcolata la frequenza dei fotogrammi media, in base al tempo trascorso corrente e al numero complessivo di frame su cui viene eseguito il rendering.  
  
 [!code-csharp[CompositionTargetSample#CompositionTarget2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CompositionTargetSample/CSharp/Window1.xaml.cs#compositiontarget2)]
 [!code-vb[CompositionTargetSample#CompositionTarget2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CompositionTargetSample/visualbasic/window1.xaml.vb#compositiontarget2)]  
  
 Si potrebbe scoprire che il disegno personalizzato viene eseguito a velocità diverse nei differenti computer.  Questa situazione si verifica in quanto il disegno personalizzato non è indipendente dalla frequenza di aggiornamento.  A seconda del sistema in esecuzione e del carico di lavoro di quel sistema, l'evento <xref:System.Windows.Media.CompositionTarget.Rendering> può essere chiamato un numero diverso di volte al secondo.  Per informazioni sulla determinazione delle funzionalità e delle prestazioni dell'hardware grafico per un dispositivo che esegue un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Livelli di rendering della grafica](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md).  
  
 L'aggiunta o la rimozione di un delegato <xref:System.EventHandler> di rendering mentre è in corso la generazione dell'evento sarà ritardata fino al completamento della generazione dell'evento.  Tale situazione è coerente con la modalità in cui vengono gestiti gli eventi basati su <xref:System.MulticastDelegate> in Common Language Runtime \(CLR\).  Notare inoltre che non si garantisce che gli eventi di rendering vengano chiamati in un particolare ordine.  Se dispone di più delegati <xref:System.EventHandler> che si basano su un ordine particolare, è necessario registrare un solo evento <xref:System.Windows.Media.CompositionTarget.Rendering> ed eseguire il multiplexing dei delegati nell'ordine corretto in modo autonomo.  
  
## Vedere anche  
 <xref:System.Windows.Media.CompositionTarget>   
 [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)