---
title: "Procedura: modificare colonne e righe utilizzando ColumnDefinitionsCollection e RowDefinitionsCollection | Microsoft Docs"
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
  - "classi, ColumnDefinitionCollection"
  - "classi, RowDefinitionCollection"
  - "ColumnDefinitionCollection (classe)"
  - "controlli, Grid (classe)"
  - "Grid (controllo), ColumnDefinitionCollection (classe)"
  - "Grid (controllo), RowDefinitionCollection (classe)"
  - "RowDefinitionCollection (classe)"
ms.assetid: bfc7160a-45f2-4e17-9961-df414dfb13c5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: modificare colonne e righe utilizzando ColumnDefinitionsCollection e RowDefinitionsCollection
In questo esempio viene illustrato come utilizzare i metodi nelle classi <xref:System.Windows.Controls.ColumnDefinitionCollection> e <xref:System.Windows.Controls.RowDefinitionCollection> per eseguire azioni come l'aggiunta, la cancellazione, o il conteggio del contenuto di righe o colonne.  Ad esempio, è possibile applicare il metodo <xref:System.Windows.Controls.ColumnDefinitionCollection.Add%2A>, <xref:System.Windows.Controls.ColumnDefinitionCollection.Clear%2A> o <xref:System.Windows.Controls.ColumnDefinitionCollection.Count%2A> agli elementi inclusi in un oggetto <xref:System.Windows.Controls.ColumnDefinition> o <xref:System.Windows.Controls.RowDefinition>.  
  
## Esempio  
 Nell'esempio seguente viene creato un elemento <xref:System.Windows.Controls.Grid> con una proprietà <xref:System.Windows.FrameworkElement.Name%2A> impostata su `grid1`.  L'oggetto <xref:System.Windows.Controls.Grid> contiene un oggetto <xref:System.Windows.Controls.StackPanel> che include elementi <xref:System.Windows.Controls.Button>, ognuno controllato da un metodo di raccolta diverso.  Quando si fa clic su un elemento <xref:System.Windows.Controls.Button>, viene attivata una chiamata a un metodo nel file code\-behind.  
  
 [!code-xml[ColumnDefinitionsGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ColumnDefinitionsGrid/CSharp/Window1.xaml#1)]  
  
 In questo esempio viene definita una serie di metodi personalizzati, ognuno corrispondente a un evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> nel file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  È possibile modificare il numero di colonne e righe nell'oggetto <xref:System.Windows.Controls.Grid> in diversi modi, ad esempio aggiungendo o rimuovendo righe e colonne nonché conteggiando il numero totale di righe e colonne.  Per evitare eccezioni <xref:System.ArgumentOutOfRangeException> e <xref:System.ArgumentException>, è possibile utilizzare la funzionalità di controllo errori fornita dal metodo <xref:System.Windows.Controls.ColumnDefinitionCollection.RemoveRange%2A>.  
  
 [!code-csharp[ColumnDefinitionsGrid#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ColumnDefinitionsGrid/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ColumnDefinitionsGrid#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ColumnDefinitionsGrid/VisualBasic/Window1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.Controls.ColumnDefinitionCollection>   
 <xref:System.Windows.Controls.RowDefinitionCollection>