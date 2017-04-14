---
title: "Procedura: eseguire l&#39;associazione a un&#39;enumerazione | Microsoft Docs"
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
  - "associazione dati, enumerazione"
  - "associazione dati, enumerazione"
  - "enumerazione"
ms.assetid: b9091eba-1119-424e-868b-d1a4168b3732
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: eseguire l&#39;associazione a un&#39;enumerazione
In questo esempio viene illustrato come associare un'enumerazione tramite l'associazione al metodo GetValues dell'enumerazione.  
  
## Esempio  
 Nell'esempio riportato di seguito, <xref:System.Windows.Controls.ListBox> consente di visualizzare l'elenco dei valori dell'enumerazione <xref:System.Windows.HorizontalAlignment> tramite l'associazione dati.  Gli oggetti <xref:System.Windows.Controls.ListBox> e <xref:System.Windows.Controls.Button> vengono associati in modo da consentire la modifica del valore della proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> di <xref:System.Windows.Controls.Button> selezionando un valore nell'oggetto <xref:System.Windows.Controls.ListBox>.  
  
 [!code-xml[BindToEnum#BindToEnum](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToEnum/CS/Window1.xaml#bindtoenum)]  
  
## Vedere anche  
 [Eseguire l'associazione a un metodo](../../../../docs/framework/wpf/data/how-to-bind-to-a-method.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)