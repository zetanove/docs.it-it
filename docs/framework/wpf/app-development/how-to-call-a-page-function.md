---
title: "Procedura: chiamare una funzione di pagina | Microsoft Docs"
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
  - "chiamata di funzioni di pagina"
  - "funzioni, chiamata"
  - "funzioni di pagina, chiamata"
ms.assetid: a4808397-c6d5-406a-83e0-0091f0c15ae4
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: chiamare una funzione di pagina
In questo esempio viene mostrato come chiamare una funzione di pagina da una pagina [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
## Esempio  
 È possibile spostarsi su una funzione di pagina utilizzando un [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)], nello stesso modo in cui ci si sposta su una pagina.  Questa operazione viene mostrata nell'esempio seguente.  
  
 [!code-csharp[HOWTOPageFunctionSnippets#NavigateToAPageFunctionLikeAPageCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/CSharp/CallingPage.xaml.cs#navigatetoapagefunctionlikeapagecodebehind)]
 [!code-vb[HOWTOPageFunctionSnippets#NavigateToAPageFunctionLikeAPageCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/VisualBasic/CallingPage.xaml.vb#navigatetoapagefunctionlikeapagecodebehind)]  
  
 Se è necessario passare i dati alla funzione di pagina, è possibile crearne un'istanza e passare i dati impostando una proprietà.  Oppure, come mostrato nell'esempio seguente, è possibile passare i dati utilizzando un costruttore non predefinito.  
  
 [!code-xml[HOWTOPageFunctionSnippets#CallAPageFunctionXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/CSharp/CallingPage.xaml#callapagefunctionxaml)]  
  
 [!code-csharp[HOWTOPageFunctionSnippets#CallAPageFunctionCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/CSharp/CallingPage.xaml.cs#callapagefunctioncodebehind)]
 [!code-vb[HOWTOPageFunctionSnippets#CallAPageFunctionCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/VisualBasic/CallingPage.xaml.vb#callapagefunctioncodebehind)]  
  
## Vedere anche  
 <xref:System.Windows.Navigation.PageFunction%601>