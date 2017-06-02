---
title: "Procedura: rilevare il momento in cui &#232; stato premuto il tasto INVIO | Microsoft Docs"
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
  - "INVIO (tasto), rilevamento"
  - "chiavi, INVIO"
ms.assetid: a66f39d2-ef4a-43a5-b454-a4ea0fe88655
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: rilevare il momento in cui &#232; stato premuto il tasto INVIO
In questo esempio viene mostrato come rilevare il momento in cui è stato premuto il tasto <xref:System.Windows.Input.Key> della tastiera.  
  
 In questo esempio sono presenti un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e un file code\-behind.  
  
## Esempio  
 Quando l'utente preme il tasto <xref:System.Windows.Input.Key> nell'oggetto <xref:System.Windows.Controls.TextBox>, l'input della casella di testo viene visualizzato in un'altra area dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  
  
 La sintassi [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] seguente crea l'interfaccia utente costituita dagli oggetti <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.TextBlock> e <xref:System.Windows.Controls.TextBox>.  
  
 [!code-xml[keydown#KeyDownUI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml#keydownui)]  
  
 Nel code\-behind seguente viene creato il gestore eventi <xref:System.Windows.UIElement.KeyDown>.  Se si preme il tasto <xref:System.Windows.Input.Key>, viene visualizzato un messaggio nell'oggetto <xref:System.Windows.Controls.TextBlock>.  
  
 [!code-csharp[keydown#KeyDownSample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml.cs#keydownsample)]
 [!code-vb[keydown#KeyDownSample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/KeyDown/VisualBasic/Window1.xaml.vb#keydownsample)]  
  
## Vedere anche  
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)