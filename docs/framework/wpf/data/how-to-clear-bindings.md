---
title: "Procedura: cancellare associazioni | Microsoft Docs"
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
  - "associazioni, cancellazione"
  - "cancellazione di associazioni"
  - "associazione dati, cancellazione di associazioni"
ms.assetid: 73962a93-32a9-4bcd-9240-bcfbb239093a
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: cancellare associazioni
In questo esempio viene illustrata la procedura per cancellare le associazioni da un oggetto.  
  
## Esempio  
 Per cancellare un'associazione da una singola proprietà in un oggetto, chiamare il metodo <xref:System.Windows.Data.BindingOperations.ClearBinding%2A>, come illustrato nella figura riportata di seguito.  Nell'esempio riportato di seguito viene rimossa l'associazione dalla proprietà <xref:System.Windows.Controls.TextBlock.TextProperty> di *mytext*, un oggetto <xref:System.Windows.Controls.TextBlock>.  
  
 [!code-csharp[CodeOnlyBinding#ClearBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#clearbinding)]
 [!code-vb[CodeOnlyBinding#ClearBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#clearbinding)]  
  
 La cancellazione rimuove l'associazione, in modo che il valore della [proprietà di dipendenza](GTMT) venga modificato su quello che avrebbe assunto senza l'associazione.  Questo valore può essere un valore predefinito, ereditato o ottenuto da un'associazione di modelli di dati.  
  
 Per cancellare le associazioni da tutte le possibili proprietà in un oggetto, utilizzare <xref:System.Windows.Data.BindingOperations.ClearAllBindings%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Data.BindingOperations>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)