---
title: "Procedura: posizionare un menu di scelta rapida personalizzato in un controllo RichTextBox | Microsoft Docs"
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
  - "menu di scelta rapida personalizzato, posizionamento"
  - "posizionamento di menu di scelta rapida personalizzati"
  - "RichTextBox (controllo), il posizionamento di menu di scelta rapida personalizzato"
  - "menu di scelta rapida, posizionamento"
ms.assetid: bf77c930-a546-4573-9a56-9af345ba189a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: posizionare un menu di scelta rapida personalizzato in un controllo RichTextBox
In questo esempio viene illustrato come posizionare un menu di scelta rapida personalizzato per un <xref:System.Windows.Controls.RichTextBox>.  
  
 Quando si implementa un menu di scelta rapida personalizzato per un **RichTextBox**, si è responsabili della gestione del posizionamento del menu di scelta rapida.  Per impostazione predefinita, un menu di scelta rapida personalizzato viene aperto al centro del **RichTextBox**.  
  
## <a name="example"></a>Esempio  
 Per eseguire l'override del comportamento del posizionamento predefinito, aggiungere un listener per il <xref:System.Windows.FrameworkContentElement.ContextMenuOpening> evento.  Nell'esempio seguente viene illustrato come eseguire questa operazione a livello di codice.  
  
 [!code-csharp[RichTextBox_ContextMenu#_AddListener](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_ContextMenu/CSharp/app.xaml.cs#_addlistener)]
 [!code-vb[RichTextBox_ContextMenu#_AddListener](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBox_ContextMenu/VisualBasic/app.xaml.vb#_addlistener)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata un'implementazione corrispondente <xref:System.Windows.FrameworkContentElement.ContextMenuOpening> listener di eventi.  
  
 [!code-csharp[RichTextBox_ContextMenu#_ListenerBody](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_ContextMenu/CSharp/app.xaml.cs#_listenerbody)]
 [!code-vb[RichTextBox_ContextMenu#_ListenerBody](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBox_ContextMenu/VisualBasic/app.xaml.vb#_listenerbody)]  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)