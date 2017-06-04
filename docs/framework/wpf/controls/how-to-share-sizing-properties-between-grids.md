---
title: "Procedura: condividere le propriet&#224; di ridimensionamento tra griglie | Microsoft Docs"
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
  - "Grid (controllo), condivisione del ridimensionamento dei dati di colonne"
  - "Grid (controllo), condivisione del ridimensionamento dei dati di righe"
  - "ridimensionamento di dati nei controlli Grid"
ms.assetid: a0535a6f-ff04-4b25-9912-7dd856e11044
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: condividere le propriet&#224; di ridimensionamento tra griglie
In questo esempio viene illustrato come condividere i dati di ridimensionamento di colonne e righe tra elementi <xref:System.Windows.Controls.Grid> per mantenere coerente il ridimensionamento.  
  
## Esempio  
 Nell'esempio seguente vengono introdotti due elementi <xref:System.Windows.Controls.Grid> come elementi figlio di un oggetto <xref:System.Windows.Controls.DockPanel> padre.  La [proprietà connessa](GTMT) <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> di <xref:System.Windows.Controls.Grid> è definita sull'oggetto <xref:System.Windows.Controls.DockPanel> padre.  
  
 Il valore della proprietà viene modificato utilizzando due elementi <xref:System.Windows.Controls.Button>, ognuno dei quali rappresenta uno dei valori della proprietà booleana.  Quando il valore della proprietà <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> è impostato su `true`, ogni membro colonna o riga di una proprietà <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> condivide informazioni sul ridimensionamento, indipendentemente dal contenuto di una riga o colonna.  
  
 [!code-xml[gridIssharedsizescopeProp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#1)]  
  
 ...  
  
 [!code-xml[gridIssharedsizescopeProp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 Nell'esempio code\-behind seguente sono gestiti i metodi generati dagli eventi  <xref:System.Windows.Controls.Primitives.ButtonBase.Click> del pulsante.  I risultati delle chiamate ai metodi vengono scritti negli elementi <xref:System.Windows.Controls.TextBlock> che utilizzano metodi get correlati per restituire i nuovi valori di proprietà come stringhe.  
  
 [!code-csharp[gridIssharedsizescopeProp#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml.cs#3)]
 [!code-vb[gridIssharedsizescopeProp#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gridIssharedsizescopeProp/VisualBasic/Window1.xaml.vb#3)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)