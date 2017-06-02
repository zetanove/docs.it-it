---
title: "Cenni preliminari sul controllo TextBlock | Microsoft Docs"
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
  - "controlli TextBlock"
  - "TextBlock (controllo)"
ms.assetid: 24720bca-341a-4b03-8a6b-7a678023b10a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Cenni preliminari sul controllo TextBlock
Il <xref:System.Windows.Controls.TextBlock> controllo fornisce il supporto di testo flessibile per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applicazioni. L'elemento è destinato principalmente basic [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] scenari che non richiedono più paragrafi di testo. Supporta un numero di proprietà che consentono un controllo preciso della presentazione, ad esempio <xref:System.Windows.Controls.TextBlock.FontFamily%2A>, <xref:System.Windows.Controls.TextBlock.FontSize%2A>, <xref:System.Windows.Controls.TextBlock.FontWeight%2A>, <xref:System.Windows.Controls.TextBlock.TextEffects%2A>, e <xref:System.Windows.Controls.TextBlock.TextWrapping%2A>. Contenuto di testo può essere aggiunti mediante la <xref:System.Windows.Controls.TextBlock.Text%2A> proprietà. Se utilizzato in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], il contenuto tra l'apertura e chiusura viene aggiunto in modo implicito come testo dell'elemento.  
  
 Oggetto <xref:System.Windows.Controls.TextBlock> elemento può essere creata un'istanza in poche parole utilizzando [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xml[TextBlockSnip_XAML#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBlockSnip_XAML/CS/default.xaml#2)]  
  
 Analogamente, l'utilizzo di <xref:System.Windows.Controls.TextBlock> elemento nel codice è relativamente semplice.  
  
 [!code-csharp[TextBlockSnip#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBlockSnip/CSharp/TextBlockSnips.cs#1)]
 [!code-vb[TextBlockSnip#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBlockSnip/VisualBasic/TextBlockSnips.vb#1)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.Label>