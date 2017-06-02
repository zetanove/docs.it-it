---
title: "Procedura: eseguire l&#39;associazione delle propriet&#224; di due controlli | Microsoft Docs"
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
  - "associazione delle proprietà di due controlli"
  - "controlli, associazione delle proprietà"
  - "associazione dati, associazione delle proprietà di due controlli"
ms.assetid: 06318fac-6afd-4c7d-a277-6d7ef50f47bc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eseguire l&#39;associazione delle propriet&#224; di due controlli
In questo esempio viene illustrato come associare la proprietà di un controllo di cui è stata creata un'istanza a quella di un altro utilizzando la proprietà <xref:System.Windows.Data.Binding.ElementName%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come associare la proprietà <xref:System.Windows.Controls.Panel.Background%2A> di <xref:System.Windows.Controls.Canvas> alla proprietà <xref:System.Windows.Controls.Primitives.Selector.SelectedItem%2A>.<xref:System.Windows.Controls.ContentControl.Content%2A> di <xref:System.Windows.Controls.ComboBox>:  
  
 [!code-xml[BindDptoDp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindDPtoDP/CS/Window1.xaml#1)]  
  
 Dopo il rendering, questo esempio avrà il seguente aspetto:  
  
 ![Area di disegno con uno sfondo verde](../../../../docs/framework/wpf/data/media/databindingbindingdpssample.png "DataBindingBindingDPsSample")  
  
 **Nota** La proprietà [di destinazione dell'associazione](GTMT) \(nell'esempio la proprietà <xref:System.Windows.Controls.Panel.Background%2A>\) deve essere una [proprietà di dipendenza](GTMT).  Per ulteriori informazioni, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
## Vedere anche  
 [Specificare l'origine di associazione](../../../../docs/framework/wpf/data/how-to-specify-the-binding-source.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)