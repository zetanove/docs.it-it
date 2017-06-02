---
title: "Procedura: aggiungere un gestore eventi mediante codice | Microsoft Docs"
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
  - "gestori eventi, aggiunta"
  - "XAML, aggiunta di gestori eventi"
ms.assetid: 269c61e0-6bd9-4291-9bed-1c5ee66da486
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: aggiungere un gestore eventi mediante codice
In questo esempio viene illustrato come aggiungere un gestore eventi a un elemento mediante codice.  
  
 Se si desidera aggiungere un gestore eventi a un elemento [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e la pagina del markup che contiene l'elemento è già stata caricata, è necessario aggiungere il gestore mediante codice.  In alternativa, se si sta compilando la struttura ad albero dell'elemento per un'applicazione interamente mediante codice senza dichiarare alcun elemento utilizzando [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile chiamare metodi specifici per aggiungere gestori eventi alla struttura ad albero dell'elemento costruita.  
  
## Esempio  
 Nell'esempio riportato di seguito viene aggiunto un nuovo oggetto <xref:System.Windows.Controls.Button> a una pagina esistente definita inizialmente in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Un file code\-behind implementa un metodo del gestore eventi, quindi aggiunge tale metodo come nuovo gestore eventi in <xref:System.Windows.Controls.Button>.  
  
 Nell'esempio di [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] viene utilizzato l'operatore `+=` per assegnare un gestore a un evento.  Si tratta dello stesso operatore utilizzato per assegnare un gestore nel modello di gestione eventi [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] non supporta questo operatore come mezzo per l'aggiunta di gestori eventi.  Richiede invece una delle due tecniche seguenti:  
  
-   Utilizzare il metodo <xref:System.Windows.UIElement.AddHandler%2A>, con un operatore `AddressOf`, per fare riferimento all'implementazione del gestore eventi.  
  
-   Utilizzare la parola chiave `Handles` come parte della definizione del gestore eventi.  Questa tecnica non viene illustrata in questo argomento; vedere [Visual Basic e la gestione degli eventi WPF](../../../../docs/framework/wpf/advanced/visual-basic-and-wpf-event-handling.md).  
  
 [!code-xml[RoutedEventAddRemoveHandler#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[RoutedEventAddRemoveHandler#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventAddRemoveHandler#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/VisualBasic/default.xaml.vb#handler)]  
  
> [!NOTE]
>  L'aggiunta di un gestore eventi nella pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] inizialmente analizzata è molto più semplice.  All'interno dell'elemento oggetto a cui si desidera aggiungere il gestore eventi, aggiungere un attributo che corrisponda al nome dell'evento da gestire.  Specificare quindi il valore di tale attributo come nome del metodo del gestore eventi definito nel file code\-behind della pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Per ulteriori informazioni, vedere [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md) o [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
## Vedere anche  
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/events-how-to-topics.md)