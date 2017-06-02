---
title: "Procedura: creare uno stile per un&#39;intestazione di colonna GridView trascinata | Microsoft Docs"
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
  - "ListView (controlli), applicazione di stili"
ms.assetid: 0b999645-0313-4b33-80b9-19ece08b5459
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare uno stile per un&#39;intestazione di colonna GridView trascinata
In questo esempio viene illustrato come modificare l'aspetto di una classe <xref:System.Windows.Controls.GridViewColumnHeader> trascinata quando l'utente modifica la posizione di una colonna.  
  
## Esempio  
 Quando si trascina un'intestazione di colonna in un altro percorso in una classe <xref:System.Windows.Controls.ListView> che utilizza <xref:System.Windows.Controls.GridView> per la modalità di visualizzazione, la colonna si sposta nella nuova posizione.  Mentre si trascina l'intestazione di colonna, oltre all'intestazione originale viene visualizzata una copia mobile dell'intestazione.  Un'intestazione di colonna in un oggetto <xref:System.Windows.Controls.GridView> è rappresentata da un oggetto <xref:System.Windows.Controls.GridViewColumnHeader>.  
  
 Per personalizzare l'aspetto delle intestazioni originali e mobili, è possibile impostare la proprietà <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> per modificare la classe <xref:System.Windows.Style> di <xref:System.Windows.Controls.GridViewColumnHeader>.  Le proprietà <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> vengono applicate quando il valore della proprietà <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> è `true` e il valore della proprietà <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> è <xref:System.Windows.Controls.GridViewColumnHeaderRole>.  
  
 Quando l'utente tiene premuto il pulsante del mouse con il mouse posizionato sull'oggetto <xref:System.Windows.Controls.GridViewColumnHeader>, il valore della proprietà <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> viene modificato in `true`.  Allo stesso modo, quando l'utente inizia l'operazione di trascinamento, la proprietà <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> viene modificata in <xref:System.Windows.Controls.GridViewColumnHeaderRole>.  
  
 Nell'esempio riportato di seguito viene illustrato come impostare <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> per modificare i colori delle proprietà <xref:System.Windows.Controls.Control.Foreground%2A> e <xref:System.Windows.Controls.Control.Background%2A> delle intestazioni originali e mobili quando l'utente trascina una colonna in una nuova posizione.  
  
 [!code-xml[ListViewHeaderRoleStyle#GVCHControlTemplateStart](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplatestart)]  
[!code-xml[ListViewHeaderRoleStyle#ControlTemplateTriggersStart](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersstart)]  
[!code-xml[ListViewHeaderRoleStyle#IsPressed](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#ispressed)]  
[!code-xml[ListViewHeaderRoleStyle#Floating](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#floating)]  
[!code-xml[ListViewHeaderRoleStyle#ControlTemplateTriggersEnd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersend)]  
[!code-xml[ListViewHeaderRoleStyle#GVCHControlTemplateEnd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplateend)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.GridViewColumnHeader>   
 <xref:System.Windows.Controls.GridViewColumnHeaderRole>   
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)