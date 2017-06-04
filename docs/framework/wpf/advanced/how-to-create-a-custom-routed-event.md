---
title: "Procedura: creare un evento indirizzato personalizzato | Microsoft Docs"
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
  - "creazione, eventi indirizzati"
  - "eventi, routing"
  - "eventi indirizzati, creazione"
ms.assetid: b79f459a-1c3f-4045-b2d4-1659cc8eaa3c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: creare un evento indirizzato personalizzato
Affinché l'evento personalizzato supporti il [routing degli eventi](GTMT), è necessario registrare un oggetto <xref:System.Windows.RoutedEvent> utilizzando il metodo <xref:System.Windows.EventManager.RegisterRoutedEvent%2A>.  In questo esempio vengono illustrate le nozioni di base per la creazione di un evento indirizzato personalizzato.  
  
## Esempio  
 Come mostrato nell'esempio seguente, è necessario innanzi tutto registrare un oggetto <xref:System.Windows.RoutedEvent> utilizzando il metodo <xref:System.Windows.EventManager.RegisterRoutedEvent%2A>.  Per convenzione, il nome del campo statico <xref:System.Windows.RoutedEvent> deve terminare con il suffisso ***Event*** In questo esempio, il nome dell'evento è `Tap` e la strategia di routing dell'evento è <xref:System.Windows.RoutingStrategy>.  Dopo la chiamata di registrazione, è possibile fornire funzioni di accesso di aggiunta e rimozione dell'evento [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] per l'evento.  
  
 Si noti che anche se l'evento viene generato tramite il metodo virtuale `OnTap` in questo particolare esempio, la modalità di generazione dell'evento o la relativa risposta alle modifiche varierà in base alle esigenze.  
  
 In questo esempio inoltre viene implementata un'intera sottoclasse di <xref:System.Windows.Controls.Button>; tale sottoclasse è compilata come assembly separato e ne viene quindi creata un'istanza come classe personalizzata in una pagina [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] separata.  Ciò vale a dimostrare che i controlli sottoclassati possono essere inseriti in strutture ad albero composte di altri controlli e che, in una situazione del genere, gli eventi personalizzati su questi controlli dispongono delle stesse funzionalità di routing di qualsiasi elemento [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] nativo.  
  
 [!code-csharp[RoutedEventCustom#CustomClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/SDKSampleLibrary/class1.cs#customclass)]
 [!code-vb[RoutedEventCustom#CustomClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventCustom/VB/SDKSampleLibrary/Class1.vb#customclass)]  
  
 [!code-xml[RoutedEventCustom#Page](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/RoutedEventCustomApp/default.xaml#page)]  
  
 Gli eventi di tunneling sono creati con la stessa modalità, ma impostando la proprietà <xref:System.Windows.RoutedEvent.RoutingStrategy%2A> su <xref:System.Windows.RoutingStrategy> nella chiamata di registrazione.  Per convenzione, gli eventi di tunneling in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono denominati con il prefisso "Preview".  
  
 Per un esempio di funzionamento degli eventi di bubbling, vedere [Gestire un evento indirizzato](../../../../docs/framework/wpf/advanced/how-to-handle-a-routed-event.md).  
  
## Vedere anche  
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md)