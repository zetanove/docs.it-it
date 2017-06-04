---
title: "Procedura: creare un effetto di testo | Microsoft Docs"
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
  - "tipo linea di base"
  - "tipi di carattere, di base"
  - "tipi di carattere, linea sopra"
  - "tipi di carattere, barrato"
  - "tipi di carattere, sottolineato"
  - "tipo linea sopra"
  - "tipo barrato"
  - "testo, decorazioni"
  - "tipografia, decorazioni di testo"
  - "tipo sottolineato"
ms.assetid: cf3cb4e7-782a-4be7-b2d4-e0935e21e4e0
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare un effetto di testo
Un oggetto <xref:System.Windows.TextDecoration> rappresenta un ornamento visivo che è possibile aggiungere al testo.  Sono disponibili quattro tipi di effetti di testo: sottolineato, linea di base, barrato e linea sopra.  Nel seguente esempio vengono mostrate le posizioni di tali effetti in relazione al testo.  
  
 ![Diagramma della posizione delle decorazioni di testo](../../../../docs/framework/wpf/advanced/media/textdecoration01.png "TextDecoration01")  
Esempio dei vari tipi di effetti di testo  
  
 Per aggiungere un effetto al testo, creare un oggetto <xref:System.Windows.TextDecoration> e modificarne le proprietà.  Utilizzare la proprietà <xref:System.Windows.TextDecoration.Location%2A> per specificare la posizione in cui sarà visualizzato l'effetto di testo, ad esempio la sottolineatura.  Utilizzare la proprietà <xref:System.Windows.TextDecoration.Pen%2A> per specificare l'aspetto dell'effetto di testo, ad esempio riempimento a tinta unita o sfumatura di colore.  Se non viene specificato alcun valore per la proprietà <xref:System.Windows.TextDecoration.Pen%2A>, gli effetti saranno impostati in modalità predefinita sullo stesso colore del testo.  Una volta definito un oggetto <xref:System.Windows.TextDecoration>, aggiungerlo alla raccolta <xref:System.Windows.TextDecorations> dell'oggetto di testo desiderato.  
  
 Nell'esempio riportato di seguito viene mostrato un effetto di testo disegnato con un pennello a sfumatura lineare e una penna tratteggiata.  
  
 ![Decorazione di testo con sottolineatura sfumata lineare](../../../../docs/framework/wpf/advanced/media/textdecoration02.png "TextDecoration02")  
Esempio di sottolineatura disegnata con un pennello a sfumatura lineare e una penna tratteggiata  
  
 L'oggetto <xref:System.Windows.Documents.Hyperlink> è un elemento del contenuto del flusso di livello inline che consente di ospitare collegamenti ipertestuali all'interno del contenuto del flusso.  Per impostazione predefinita, <xref:System.Windows.Documents.Hyperlink> utilizza un oggetto <xref:System.Windows.TextDecoration> per visualizzare una sottolineatura.  Gli oggetti <xref:System.Windows.TextDecoration> possono essere prestazione intensive da creare, in particolare se si hanno molti oggetti <xref:System.Windows.Documents.Hyperlink>.  Se gli elementi <xref:System.Windows.Documents.Hyperlink>, utilizzati sono molti è opportuno visualizzare una sottolineatura solo al momento della generazione di un evento, ad esempio l'evento <xref:System.Windows.ContentElement.MouseEnter>.  
  
 Nell'esempio riportato di seguito, il collegamento "My MSN" presenta una sottolineatura dinamica, vale a dire che la sottolineatura viene visualizzata solo al momento della generazione dell'evento <xref:System.Windows.ContentElement.MouseEnter>.  
  
 ![Collegamenti ipertestuali con TextDecoration](../../../../docs/framework/wpf/advanced/media/textdecoration03.png "TextDecoration03")  
Collegamenti ipertestuali definiti con TextDecorations  
  
 Per ulteriori informazioni, vedere [Specificare se un collegamento ipertestuale è sottolineato](../../../../docs/framework/wpf/advanced/how-to-specify-whether-a-hyperlink-is-underlined.md).  
  
## Esempio  
 Nel codice seguente, un effetto di testo con sottolineatura utilizza il valore del tipo di carattere predefinito.  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets1)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets1)]
 [!code-xml[TextDecorationSnippets#TextDecorationSnippets1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets1)]  
  
 Nel seguente esempio di codice, viene creato un effetto di testo con sottolineatura mediante l'utilizzo di un pennello a tinta unita per la penna.  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets2)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets2)]
 [!code-xml[TextDecorationSnippets#TextDecorationSnippets2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets2)]  
  
 Nell'esempio di codice seguente, viene creato un effetto di testo con sottolineatura utilizzando un pennello a sfumatura lineare per la penna tratteggiata.  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets3)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets3)]
 [!code-xml[TextDecorationSnippets#TextDecorationSnippets3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets3)]  
  
## Vedere anche  
 <xref:System.Windows.TextDecoration>   
 <xref:System.Windows.Documents.Hyperlink>   
 [Specificare se un collegamento ipertestuale è sottolineato](../../../../docs/framework/wpf/advanced/how-to-specify-whether-a-hyperlink-is-underlined.md)