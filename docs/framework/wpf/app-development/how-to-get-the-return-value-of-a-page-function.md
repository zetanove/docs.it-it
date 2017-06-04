---
title: "Procedura: ottenere il valore restituito di una funzione di pagina | Microsoft Docs"
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
  - "funzioni, recupero di valori restituiti"
  - "recupero, valori restituiti dalle funzioni di pagina"
  - "funzioni di pagina, recupero di valori restituiti"
  - "valori restituiti dalle funzioni di pagina"
ms.assetid: 75470af6-256c-4c46-87e7-705080723a1c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: ottenere il valore restituito di una funzione di pagina
In questo esempio viene mostrato come ottenere il risultato restituito da una funzione di pagina.  
  
## Esempio  
 Per ottenere il risultato restituito da una funzione di pagina è necessario gestire l'evento <xref:System.Windows.Navigation.PageFunction%601.Return> della funzione di pagina che si chiama.  
  
 [!code-xml[HOWTOPageFunctionSnippets#CallAPageFunctionXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/CSharp/CallingPage.xaml#callapagefunctionxaml)]  
  
 [!code-csharp[HOWTOPageFunctionSnippets#GetPageFunctionResultCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/CSharp/CallingPage.xaml.cs#getpagefunctionresultcodebehind)]
 [!code-vb[HOWTOPageFunctionSnippets#GetPageFunctionResultCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOPageFunctionSnippets/VisualBasic/CallingPage.xaml.vb#getpagefunctionresultcodebehind)]  
  
## Vedere anche  
 <xref:System.Windows.Navigation.PageFunction%601>