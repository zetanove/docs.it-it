---
title: "Procedura: eseguire l&#39;override dell&#39;albero logico | Microsoft Docs"
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
  - "albero logico, override"
  - "override dell'albero logico"
ms.assetid: 0ae4d074-8113-4b06-b4fa-e0f39d4967a6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: eseguire l&#39;override dell&#39;albero logico
Benché non sia necessario nella maggior parte dei casi, gli autori di controlli avanzati possono eseguire l'override dell'[albero logico](GTMT).  
  
## Esempio  
 In questo esempio viene descritto come creare una sottoclasse di <xref:System.Windows.Controls.StackPanel> per eseguire l'override dell'albero logico, in questo caso per imporre un comportamento per il quale un pannello può disporre e può eseguire il rendering di un solo elemento figlio.  Benché non si tratta necessariamente di un comportamento utile, viene presentato come mezzo per illustrare lo scenario di override dell'albero logico normale di un elemento.  
  
 [!code-csharp[LogicalOverride#SingletonPanel](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LogicalOverride/CSharp/SDKSampleLibrary/class1.cs#singletonpanel)]  
  
 Per ulteriori informazioni sull'albero logico, vedere [Strutture ad albero in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md).