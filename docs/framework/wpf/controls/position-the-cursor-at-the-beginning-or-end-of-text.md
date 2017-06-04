---
title: "Procedura: posizionare il cursore all&#39;inizio o alla fine del testo in un controllo TextBox | Microsoft Docs"
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
  - "posizionamento del cursore"
  - "Controllo TextBox, posizionamento del cursore"
  - "cursore, posizionamento"
ms.assetid: c771a0b8-c6b4-4240-aecd-a21d0ba51a2e
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: posizionare il cursore all&#39;inizio o alla fine del testo in un controllo TextBox
In questo esempio viene illustrato come posizionare il cursore all'inizio o alla fine del contenuto di testo di un <xref:System.Windows.Controls.TextBox> controllo.  
  
## <a name="example"></a>Esempio  
 Nell'esempio [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] codice descrive un <xref:System.Windows.Controls.TextBox> controllare e assegna un nome.  
  
 [!code-xml[TextBox_MiscCode#_MoveCursorXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_movecursorxaml)]  
  
## <a name="example"></a>Esempio  
 Posizionare il cursore all'inizio del contenuto di un <xref:System.Windows.Controls.TextBox> di controllo, chiamare il <xref:System.Windows.Controls.TextBox.Select%2A> metodo e specificare la posizione iniziale pari a 0 e una lunghezza pari a 0.  
  
 [!code-csharp[TextBox_MiscCode#_CursorToStart](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_cursortostart)]
 [!code-vb[TextBox_MiscCode#_CursorToStart](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_cursortostart)]  
  
## <a name="example"></a>Esempio  
 Posizionare il cursore alla fine del contenuto di un <xref:System.Windows.Controls.TextBox> di controllo, chiamare il <xref:System.Windows.Controls.TextBox.Select%2A> metodo e specificare la posizione iniziale uguale alla lunghezza del contenuto di testo e una lunghezza pari a 0.  
  
 [!code-csharp[TextBox_MiscCode#_CursorToEnd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_cursortoend)]
 [!code-vb[TextBox_MiscCode#_CursorToEnd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_cursortoend)]  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni preliminari sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)