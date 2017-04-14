---
title: "Procedura: creare associazioni semplici | Microsoft Docs"
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
  - "associazione dati, creazione di associazioni semplici"
  - "associazione semplice, creazione"
ms.assetid: 69b80f72-6259-44cb-8294-5bdcebca1e08
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: creare associazioni semplici
In questo esempio viene illustrato come creare un oggetto <xref:System.Windows.Data.Binding> semplice.  
  
## Esempio  
 In questo esempio, è presente un oggetto `Person` con una proprietà stringa denominata `PersonName`.  L'oggetto `Person` è definito nello spazio dei nomi `SDKSample`.  
  
 Nell'esempio riportato di seguito viene creata un'istanza dell'oggetto `Person` con un valore della proprietà `PersonName` uguale a `Joe`.  Questa operazione viene eseguita nella sezione `Resources` e viene assegnato `x:Key`.  
  
 [!code-xml[SimpleBinding#Instantiation](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#instantiation)]  
[!code-xml[SimpleBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#2)]  
[!code-xml[SimpleBinding#EndWindow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#endwindow)]  
  
 Per eseguire l'associazione alla proprietà `PersonName`, eseguire le seguenti operazioni:  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 Il risultato dell'operazione è la visualizzazione dell'oggetto <xref:System.Windows.Controls.TextBlock> con il valore "Joe".  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)