---
title: "Procedura: creare uno StackPanel | Microsoft Docs"
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
  - "StackPanel (controllo), creazione"
ms.assetid: e7ce65cb-720a-4bb6-95b6-286b74488a58
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: creare uno StackPanel
In questo esempio viene illustrato come creare un <xref:System.Windows.Controls.StackPanel>.  
  
## <a name="example"></a>Esempio  
 Oggetto <xref:System.Windows.Controls.StackPanel> consente di sovrapporre gli elementi in una direzione specificata. Utilizzando le proprietà definite su <xref:System.Windows.Controls.StackPanel>, il contenuto può fluire in verticale, ovvero l'impostazione predefinita, orizzontalmente o verticalmente.  
  
 Nell'esempio seguente uno stack verticale cinque <xref:System.Windows.Controls.TextBlock> controlli, ognuno con un altro <xref:System.Windows.Controls.Border> e <xref:System.Windows.Controls.Border.Background%2A>, utilizzando <xref:System.Windows.Controls.StackPanel>. Gli elementi figlio che non hanno alcuna specificato <xref:System.Windows.FrameworkElement.Width%2A> adattata per riempire la finestra padre; tuttavia, gli elementi figlio con un determinato <xref:System.Windows.FrameworkElement.Width%2A>, centrata all'interno della finestra.  
  
 La direzione dello stack predefinita in un <xref:System.Windows.Controls.StackPanel> è verticale. Per controllare il flusso del contenuto in un <xref:System.Windows.Controls.StackPanel>, utilizzare il <xref:System.Windows.Controls.StackPanel.Orientation%2A> proprietà. È possibile controllare l'allineamento orizzontale utilizzando il <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> proprietà.  
  
```xaml  
  
<Page xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" WindowTitle="StackPanel Sample">  
  <StackPanel>  
    <Border Background="SkyBlue" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="12">Stacked Item #1</TextBlock>  
    </Border>  
    <Border Width="400" Background="CadetBlue" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="14">Stacked Item #2</TextBlock>  
    </Border>  
    <Border Background="LightGoldenRodYellow" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="16">Stacked Item #3</TextBlock>  
    </Border>  
    <Border Width="200" Background="PaleGreen" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="18">Stacked Item #4</TextBlock>  
    </Border>  
    <Border Background="White" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="20">Stacked Item #5</TextBlock>  
    </Border>  
  </StackPanel>  
</Page>  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.StackPanel>   
 [Panoramica di pannelli](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Procedure](../../../../docs/framework/wpf/controls/stackpanel-how-to-topics.md)