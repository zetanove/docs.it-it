---
title: "Procedura: ottenere l&#39;oggetto di associazione da una propriet&#224; di destinazione associata | Microsoft Docs"
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
  - "associazione dati, recupero di oggetti di associazione da proprietà di destinazione associate"
  - "proprietà, recupero di oggetti di associazione"
ms.assetid: 87974c5f-136b-4de7-b07d-9285b62ab123
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: ottenere l&#39;oggetto di associazione da una propriet&#224; di destinazione associata
In questo esempio viene illustrato come ottenere l'oggetto di associazione da una proprietà di destinazione associata ai dati.  
  
## Esempio  
 Per ottenere un oggetto <xref:System.Windows.Data.Binding>, effettuare l'operazione riportata di seguito.  
  
 [!code-csharp[BindValidation#GetBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml.cs#getbinding)]  
  
> [!NOTE]
>  È necessario specificare la [proprietà di dipendenza](GTMT) per l'associazione desiderata poiché è possibile che l'associazione dati sia utilizzata da più proprietà dell'oggetto di destinazione.  
  
 In alternativa, è possibile ottenere <xref:System.Windows.Data.BindingExpression> e quindi il valore della proprietà <xref:System.Windows.Data.BindingExpression.ParentBinding%2A>.  
  
 Per l'esempio completo, vedere [Esempio Binding Validation](http://go.microsoft.com/fwlink/?LinkID=159972) \(la pagina potrebbe essere in inglese\).  
  
> [!NOTE]
>  Se l'associazione è <xref:System.Windows.Data.MultiBinding>, utilizzare <xref:System.Windows.Data.BindingOperations>.<xref:System.Windows.Data.BindingOperations.GetMultiBinding%2A>,  se è <xref:System.Windows.Data.PriorityBinding>, utilizzare <xref:System.Windows.Data.BindingOperations>.<xref:System.Windows.Data.BindingOperations.GetPriorityBinding%2A>.  Se non si è certi se la proprietà di destinazione sia associata utilizzando <xref:System.Windows.Data.Binding>, <xref:System.Windows.Data.MultiBinding> o <xref:System.Windows.Data.PriorityBinding>, è possibile utilizzare <xref:System.Windows.Data.BindingOperations>.<xref:System.Windows.Data.BindingOperations.GetBindingBase%2A>.  
  
## Vedere anche  
 [Creare un'associazione nel codice](../../../../docs/framework/wpf/data/how-to-create-a-binding-in-code.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)