---
title: "Procedura: implementare la logica di convalida negli oggetti personalizzati | Microsoft Docs"
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
  - "controllo degli errori di convalida [WPF]"
  - "oggetti personalizzati [WPF], implementazione della logica di convalida"
  - "implementazione della logica di convalida in oggetti personalizzati [WPF]"
  - "errori di convalida [WPF], controllo"
ms.assetid: 751fda9b-44f9-4d63-b4f2-1df07ac41e0f
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: implementare la logica di convalida negli oggetti personalizzati
In questo esempio viene illustrato come implementare la logica di convalida in un oggetto personalizzato ed eseguire l'associazione a tale oggetto.  
  
## Esempio  
 È possibile fornire la logica di convalida a livello aziendale se l'oggetto di origine implementa <xref:System.ComponentModel.IDataErrorInfo>, come nell'esempio seguente:  
  
 [!code-csharp[BusinessLayerValidation#IDataErrorInfo](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Data.cs#idataerrorinfo)]
 [!code-vb[BusinessLayerValidation#IDataErrorInfo](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BusinessLayerValidation/VisualBasic/Data.vb#idataerrorinfo)]  
  
 Nell'esempio seguente, la proprietà Text della casella di testo viene associata alla proprietà `Age` dell'oggetto `Person`, resa disponibile per l'associazione tramite una dichiarazione della risorsa fornita dall'oggetto `data` `x:Key`.  <xref:System.Windows.Controls.DataErrorValidationRule> controlla gli errori di convalida generati dall'implementazione <xref:System.ComponentModel.IDataErrorInfo>.  
  
 [!code-xml[BusinessLayerValidation#BoundTextBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Window1.xaml#boundtextbox)]  
  
 In alternativa, anziché utilizzare <xref:System.Windows.Controls.DataErrorValidationRule>, è possibile impostare la proprietà <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> su `true`.  
  
## Vedere anche  
 <xref:System.Windows.Controls.ExceptionValidationRule>   
 [Implementare la convalida dell'associazione](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)