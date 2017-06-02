---
title: "Procedura: creare ListViewItem con un CheckBox | Microsoft Docs"
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
  - "controlli ListView"
  - "controlli, la casella di controllo"
  - "ListView (controlli), controlli CheckBox"
  - "Controllo CheckBox, controllo ListView"
ms.assetid: f6d66c7f-906c-4f65-a55a-0ede9d00e26a
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: creare ListViewItem con un CheckBox
In questo esempio viene illustrato come visualizzare una colonna di <xref:System.Windows.Controls.CheckBox> controlli in un <xref:System.Windows.Controls.ListView> controllo che utilizza un <xref:System.Windows.Controls.GridView>.  
  
## <a name="example"></a>Esempio  
 Per creare una colonna che contiene <xref:System.Windows.Controls.CheckBox> controlli in un <xref:System.Windows.Controls.ListView>, creare un <xref:System.Windows.DataTemplate> che contiene un <xref:System.Windows.Controls.CheckBox>. Impostare quindi la <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> di un <xref:System.Windows.Controls.GridViewColumn> per il <xref:System.Windows.DataTemplate>.  
  
 Nell'esempio seguente un <xref:System.Windows.DataTemplate> che contiene un <xref:System.Windows.Controls.CheckBox>. Nell'esempio viene associato il <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> proprietà del <xref:System.Windows.Controls.CheckBox> per il <xref:System.Windows.Controls.ListBoxItem.IsSelected%2A> valore della proprietà di <xref:System.Windows.Controls.ListViewItem> che lo contiene. Pertanto, quando il <xref:System.Windows.Controls.ListViewItem> che contiene il <xref:System.Windows.Controls.CheckBox> è selezionata, il <xref:System.Windows.Controls.CheckBox> è selezionata.  
  
 [!code-xml[ListViewChkBox#CheckBoxDataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#checkboxdatatemplate)]  
  
 Nell'esempio seguente viene illustrato come creare una colonna di <xref:System.Windows.Controls.CheckBox> controlli. Impostare la colonna, nell'esempio viene impostata la <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> proprietà del <xref:System.Windows.Controls.GridViewColumn> per il <xref:System.Windows.DataTemplate>.  
  
 [!code-xml[ListViewChkBox#GridViewColumnCheckBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#gridviewcolumncheckbox)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.Control>   
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Procedure](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)