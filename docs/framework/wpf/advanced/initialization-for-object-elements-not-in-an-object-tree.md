---
title: "Inizializzazione di elementi oggetto non presenti in una struttura ad albero di oggetti | Microsoft Docs"
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
  - "elementi, inizializzazione"
  - "inizializzazione di elementi"
  - "albero logico"
  - "struttura ad albero visuale"
ms.assetid: 7b8dfc9b-46ac-4ce8-b7bb-035734d688b7
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Inizializzazione di elementi oggetto non presenti in una struttura ad albero di oggetti
Alcuni aspetti dell'inizializzazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] vengono rinviati ai processi che generalmente si basano sull'elemento connesso all'[albero logico](GTMT) o alla [struttura ad albero visuale](GTMT).  In questo argomento vengono descritti i passaggi necessari per inizializzare un elemento non connesso a una delle strutture ad albero.  
  
   
  
## Elementi e albero logico  
 Quando si crea un'istanza di una classe [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] all'interno del codice, è necessario tenere presente che molti aspetti dell'inizializzazione dell'oggetto per una classe [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] non fanno deliberatamente parte del codice che viene eseguito quando si chiama il costruttore di classi.  In modo particolare per una classe di controllo, la maggior parte delle rappresentazioni visive di quel controllo non viene definita dal costruttore,  ma dal modello del controllo.  Sebbene provenga potenzialmente da diverse origini, nella maggior parte dei casi il modello viene ottenuto dagli stili dei temi.  I modelli sono effettivamente un'associazione tardiva; il modello necessario non viene associato al controllo in questione finché il controllo non è pronto per il layout  e quest'ultima situazione non si verifica finché il controllo non viene associato a un albero logico che si connette a una superficie di rendering nella radice.  È tale elemento a livello radice che avvia il rendering di tutti i relativi elementi figlio definiti nell'albero logico.  
  
 Anche la struttura ad albero visuale partecipa a questo processo.  Non viene creata un'istanza completa per gli elementi che fanno parte della struttura ad albero visuale tramite i modelli finché questi non vengono connessi.  
  
 Le conseguenze di questo comportamento sono la necessità di passaggi aggiuntivi per alcune operazioni basate sulle caratteristiche visive completate di un elemento.  Un esempio è rappresentato dal tentativo di ottenere le caratteristiche visive di una classe costruita, ma non ancora associata a una struttura ad albero.  Ad esempio, se si desidera chiamare il metodo <xref:System.Windows.Media.Imaging.RenderTargetBitmap.Render%2A> in un oggetto <xref:System.Windows.Media.Imaging.RenderTargetBitmap> e se l'elemento visivo che si sta passando è un elemento non connesso a una struttura ad albero, tale elemento non viene completato in modo visivo finché non vengono terminati ulteriori passaggi di inizializzazione.  
  
### Utilizzo di BeginInit e EndInit per inizializzare l'elemento  
 Diverse classi di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] implementano l'interfaccia <xref:System.ComponentModel.ISupportInitialize>.  Per indicare un'area del codice contenente passaggi di inizializzazione \(ad esempio l'impostazione di valori della proprietà che influiscono sul rendering\), vengono utilizzati i metodi <xref:System.ComponentModel.ISupportInitialize.BeginInit%2A> e <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> dell'interfaccia.  Dopo aver chiamato il metodo <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> nella sequenza, il sistema di layout può elaborare l'elemento e iniziare a cercare uno stile implicito.  
  
 Se l'elemento per cui si stanno impostando le proprietà è una classe derivata <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>, è possibile chiamare le versioni della classe di <xref:System.Windows.FrameworkElement.BeginInit%2A> e <xref:System.Windows.FrameworkElement.EndInit%2A>, invece di eseguire il cast sull'oggetto <xref:System.ComponentModel.ISupportInitialize>.  
  
### Codice di esempio  
 L'esempio seguente è un codice di esempio per un'applicazione console che utilizza le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di rendering e <xref:System.Windows.Markup.XamlReader.Load%28System.IO.Stream%29?displayProperty=fullName> di un file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] separato per illustrare il posizionamento corretto di <xref:System.Windows.FrameworkElement.BeginInit%2A> e di <xref:System.Windows.FrameworkElement.EndInit%2A> intorno ad altre chiamate [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] che regolano le proprietà che influiscono sul rendering.  
  
 Nell'esempio seguente viene illustrata solo la funzione principale.  Le funzioni `Rasterize` e `Save` \(non mostrate\) sono funzioni di utilità che gestiscono l'elaborazione di immagini e l'I\/O.  
  
 [!code-csharp[InitializeElements#Main](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InitializeElements/CSharp/initializeelements.cs#main)]
 [!code-vb[InitializeElements#Main](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InitializeElements/VisualBasic/initializeelements.vb#main)]  
  
## Vedere anche  
 [Strutture ad albero in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)   
 [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)