---
title: "Procedura: associare un controllo ListBox ai dati | Microsoft Docs"
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
  - "associazione dati, a un controllo ListBox"
  - "associazione dati, ListBox (controllo)"
  - "ListBox (controlli), associazione dati"
ms.assetid: de93a907-709a-44a7-84bf-578b846a3d8b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: associare un controllo ListBox ai dati
Uno sviluppatore di applicazioni può creare controlli <xref:System.Windows.Controls.ListBox> senza specificare separatamente il contenuto di ciascun oggetto <xref:System.Windows.Controls.ListBoxItem>.  Per associare i dati ai singoli elementi è possibile utilizzare l'associazione dati.  
  
 Nell'esempio seguente viene illustrato come creare un oggetto <xref:System.Windows.Controls.ListBox> che popola gli elementi <xref:System.Windows.Controls.ListBoxItem> utilizzando l'associazione dati a un'origine dati denominata *Colori*.  In questo caso, non è necessario utilizzare tag <xref:System.Windows.Controls.ListBoxItem> per specificare il contenuto di ciascun elemento.  
  
## Esempio  
 [!code-xml[ListBoxEvent#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#7)]  
[!code-xml[ListBoxEvent#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#3)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.Controls.ListBoxItem>   
 [Controlli](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)