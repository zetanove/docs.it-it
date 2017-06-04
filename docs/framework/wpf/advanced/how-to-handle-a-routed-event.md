---
title: "Procedura: gestire un evento indirizzato | Microsoft Docs"
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
  - "eventi di bubbling"
  - "eventi indirizzati, gestione"
ms.assetid: 157787b4-f469-4047-8777-5b034145f32e
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Procedura: gestire un evento indirizzato
In questo esempio viene illustrato il funzionamento degli eventi [bubbling](GTMT) e come scrivere un gestore in grado di elaborare i dati dell'[evento indirizzato](GTMT).  
  
## Esempio  
 In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], gli elementi sono disposti in una [struttura ad albero dell'elemento](GTMT).  L'elemento padre può partecipare alla gestione di eventi inizialmente generati dagli elementi figlio nella struttura ad albero dell'elemento.  Questo è possibile grazie al [routing degli eventi](GTMT).  
  
 Per gli eventi indirizzati si utilizza in genere una delle due strategie di routing seguenti: [bubbling](GTMT) o [tunneling](GTMT).  In questo esempio viene considerato l'evento [bubbling](GTMT) e viene utilizzato l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click?displayProperty=fullName> per illustrare il funzionamento del routing.  
  
 Nell'esempio riportato di seguito vengono creati due controlli <xref:System.Windows.Controls.Button> e viene utilizzata la sintassi degli attributi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] per associare un gestore eventi a un elemento padre comune, che in questo esempio è <xref:System.Windows.Controls.StackPanel>.  Anziché associare singoli gestori eventi per ogni elemento <xref:System.Windows.Controls.Button> figlio, nell'esempio viene utilizzata la sintassi degli attributi per associare il gestore eventi all'elemento <xref:System.Windows.Controls.StackPanel> padre.  Con questo modello di gestione di eventi viene illustrato in che modo utilizzare il routing di eventi come tecnica per ridurre il numero di elementi a cui è associato un gestore.  Tutti gli eventi [bubbling](GTMT) per ogni <xref:System.Windows.Controls.Button> sono indirizzati tramite l'elemento padre.  
  
 Si noti che nell'elemento <xref:System.Windows.Controls.StackPanel> padre, il nome di evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> specificato come attributo è parzialmente qualificato mediante la denominazione della classe <xref:System.Windows.Controls.Button>.  La classe <xref:System.Windows.Controls.Button> è una classe derivata <xref:System.Windows.Controls.Primitives.ButtonBase> che dispone dell'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> nel proprio elenco dei membri.  La tecnica della qualifica parziale per l'associazione di un gestore eventi è necessaria se l'evento che viene gestito non esiste nell'elenco dei membri dell'elemento a cui viene associato il gestore dell'evento indirizzato.  
  
 [!code-xml[RoutedEventHandle#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml#xaml)]  
  
 Nell'esempio riportato di seguito viene descritta la gestione dell'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click>.  Nell'esempio viene stabilito quale elemento gestisce l'evento e quale elemento genera l'evento.  Il gestore eventi viene eseguito quando l'utente fa clic su uno dei pulsanti.  
  
 [!code-csharp[RoutedEventHandle#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventHandle#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventHandle/VisualBasic/MainWindow.xaml.vb#handler)]  
  
## Vedere anche  
 <xref:System.Windows.RoutedEvent>   
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/events-how-to-topics.md)   
 [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)