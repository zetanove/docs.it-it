---
title: "Procedura: inserire un elemento in un testo a livello di codice | Microsoft Docs"
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
  - "elementi, inserimento nel testo"
  - "inserimento di elementi nel testo"
  - "Esempio di animazione testo"
  - "testo, inserimento di elementi"
  - "TextPointer (oggetti)"
ms.assetid: 97bd950a-25ac-4e42-a311-94b6420d4136
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: inserire un elemento in un testo a livello di codice
Nell'esempio riportato di seguito viene illustrato come utilizzare due oggetti <xref:System.Windows.Documents.TextPointer> per specificare un intervallo all'interno del testo a cui applicare un elemento <xref:System.Windows.Documents.Span>.  
  
## Esempio  
 [!code-csharp[FlowMiscSnippets_procedural_snip#InsertInlineIntoTextExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowMiscSnippets_procedural_snip/CSharp/InsertInlineIntoTextExample.cs#insertinlineintotextexamplewholepage)]
 [!code-vb[FlowMiscSnippets_procedural_snip#InsertInlineIntoTextExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowMiscSnippets_procedural_snip/VisualBasic/InsertInlineIntoTextExample.vb#insertinlineintotextexamplewholepage)]  
  
 Nella figura riportata di seguito viene illustrato l'esempio in esame.  
  
 ![Elemento Span applicato a un intervallo di testo](../../../../docs/framework/wpf/advanced/media/flow-insertelementintotextprogrammatically.png "Flow\_InsertElementIntoTextProgrammatically")  
  
## Vedere anche  
 [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)