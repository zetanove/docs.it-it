---
title: "Procedura: creare associazioni nel codice | Microsoft Docs"
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
  - "associazione dati, creazione"
  - "associazione dati, creazione"
ms.assetid: 1a606db9-cf5f-42ed-a1c5-9e4722ec77a0
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Procedura: creare associazioni nel codice
In questo esempio viene illustrato come creare e impostare un oggetto <xref:System.Windows.Data.Binding> nel codice.  
  
## Esempio  
 Le classi <xref:System.Windows.FrameworkElement> e <xref:System.Windows.FrameworkContentElement> espongono entrambe un metodo `SetBinding`.  Se si associa un elemento che eredita da una di queste classi, è possibile chiamare direttamente il metodo <xref:System.Windows.FrameworkElement.SetBinding%2A>.  
  
 Nell'esempio seguente viene creata una classe denominata `MyData` che contiene una proprietà denominata `MyDataProperty`.  
  
 [!code-csharp[CodeOnlyBinding#DataObject](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/MyData.cs#dataobject)]
 [!code-vb[CodeOnlyBinding#DataObject](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/MyData.vb#dataobject)]  
  
 Nell'esempio riportato di seguito viene illustrato come creare un oggetto di associazione per impostare il database di origine dell'associazione.  Nell'esempio viene utilizzato <xref:System.Windows.FrameworkElement.SetBinding%2A> per associare la proprietà <xref:System.Windows.Controls.TextBlock.Text%2A> di `myText`, che è un controllo <xref:System.Windows.Controls.TextBlock>, a `MyDataProperty`.  
  
 [!code-csharp[CodeOnlyBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#1)]
 [!code-vb[CodeOnlyBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#1)]  
  
 Per l'esempio di codice completo, vedere [Code\-only Binding Sample](http://msdn.microsoft.com/it-it/764aaf0b-2216-4941-9548-9c98da18d1a6).  
  
 Anziché chiamare <xref:System.Windows.FrameworkElement.SetBinding%2A>, è possibile utilizzare il metodo statico <xref:System.Windows.Data.BindingOperations.SetBinding%2A> della classe <xref:System.Windows.Data.BindingOperations>.  Nell'esempio seguente, viene chiamato <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=fullName> anziché <xref:System.Windows.FrameworkElement.SetBinding%2A?displayProperty=fullName> per associare `myText` a `myDataProperty`.  
  
 [!code-csharp[CodeOnlyBinding#BOSetBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#bosetbinding)]
 [!code-vb[CodeOnlyBinding#BOSetBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#bosetbinding)]  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)