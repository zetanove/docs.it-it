---
title: "Procedura: attivare l&#39;enumerazione TextTrimming | Microsoft Docs"
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
  - "documenti, rimozione di testo"
  - "testo, rimozione"
  - "rimozione di testo"
ms.assetid: dd8c9191-d2be-45fd-9fb4-3c75b65578c5
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: attivare l&#39;enumerazione TextTrimming
In questo esempio vengono illustrati l'utilizzo e gli effetti dei valori disponibili nell'enumerazione <xref:System.Windows.TextTrimming>.  
  
## Esempio  
 Nell'esempio seguente viene definito un elemento <xref:System.Windows.Controls.TextBlock> con l'attributo <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> impostato.  
  
 [!code-xml[TextTrimmingSnippets#_TextTrimmingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml#_texttrimmingxaml)]  
  
## Esempio  
 Di seguito viene illustrata l'impostazione della proprietà <xref:System.Windows.TextTrimming> corrispondente in codice.  
  
 [!code-csharp[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml.cs#_texttrimmingsettexttrimming)]
 [!code-vb[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextTrimmingSnippets/VisualBasic/Window1.xaml.vb#_texttrimmingsettexttrimming)]  
  
 Attualmente sono disponibili tre opzioni per il taglio del testo: **CharacterEllipsis**, **WordEllipsis** e **None**.  
  
 Se <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> è impostato su **CharacterEllipsis**, il testo viene tagliato e in corrispondenza del carattere più vicino al bordo del taglio vengono inseriti dei puntini di sospensione.  Tale impostazione consente di tagliare il testo in modo da adattarlo meglio al limite di taglio, ma potrebbe determinare la troncatura delle parole.  Nell'immagine seguente vengono mostrati gli effetti di questa impostazione su un oggetto <xref:System.Windows.Controls.TextBlock> analogo a quello definito in precedenza.  
  
 ![Esempio: TextTrimming.CharacterEllipsis](../../../../docs/framework/wpf/advanced/media/texttrimming-character.png "TextTrimming\_Character")  
  
 Se <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> è impostato su **WordEllipsis**, il testo viene tagliato e alla fine della prima parola completa più vicina al bordo del taglio vengono inseriti dei puntini di sospensione.  Grazie a questa impostazione le parole non risulteranno tronche, ma non è possibile tagliare il testo in prossimità del bordo di taglio come consentito dall'impostazione **CharacterEllipsis**.  Nell'immagine seguente vengono mostrati gli effetti di questa impostazione sull'oggetto <xref:System.Windows.Controls.TextBlock> definito in precedenza.  
  
 ![Esempio: TextTrimming.WordEllipsis](../../../../docs/framework/wpf/advanced/media/texttrimming-word.png "TextTrimming\_Word")  
  
 Quando <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> è impostato su **None**, non viene eseguita alcuna operazione di taglio del testo.  In questo caso, viene eseguita una semplice operazione di ritaglio in corrispondenza del limite del contenitore di testo padre.  Nell'immagine seguente vengono mostrati gli effetti di questa impostazione su un oggetto <xref:System.Windows.Controls.TextBlock> analogo a quello definito in precedenza.  
  
 ![Esempio: TextTrimming.None](../../../../docs/framework/wpf/advanced/media/texttrimming-none.png "TextTrimming\_None")