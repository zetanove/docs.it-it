---
title: "Procedura: posizionare gli elementi figlio di una griglia | Microsoft Docs"
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
  - "Grid (controllo), posizionamento di elementi figlio"
ms.assetid: 27b3ba9b-ad32-44e2-bcab-a79d573a463c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: posizionare gli elementi figlio di una griglia
In questo esempio viene illustrato come utilizzare i metodi get e set definiti sulla classe <xref:System.Windows.Controls.Grid> per posizionare elementi figlio.  
  
## Esempio  
 Nell'esempio riportato di seguito viene definito un elemento <xref:System.Windows.Controls.Grid> padre \(`grid1`\) con tre colonne e tre righe.  Un elemento <xref:System.Windows.Shapes.Rectangle> figlio \(`rect1`\) viene aggiunto all'elemento <xref:System.Windows.Controls.Grid> nella posizione di colonna zero e nella posizione di riga zero.  Gli elementi <xref:System.Windows.Controls.Button> rappresentano metodi che è possibile chiamare per riposizionare l'elemento <xref:System.Windows.Shapes.Rectangle> all'interno dell'elemento <xref:System.Windows.Controls.Grid>.  Quando un utente fa clic su un pulsante, il metodo correlato viene attivato.  
  
 [!code-xml[gridGetSetMethods#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml#1)]  
  
 Nell'esempio code\-behind seguente sono gestiti i metodi generati dagli eventi del pulsante <xref:System.Windows.Controls.Primitives.ButtonBase.Click>.  Nell'esempio le chiamate al metodo sono scritte negli elementi <xref:System.Windows.Controls.TextBlock> che utilizzano metodi get correlati per restituire i nuovi valori di proprietà come stringhe.  
  
 [!code-csharp[gridGetSetMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[gridGetSetMethods#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gridGetSetMethods/VisualBasic/Window1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Grid>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)