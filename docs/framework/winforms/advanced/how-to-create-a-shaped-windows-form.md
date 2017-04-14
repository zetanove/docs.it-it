---
title: "Procedura: creare un Windows Form con una forma | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "form, modifica della forma"
  - "form, circolari"
  - "form, forme personalizzate"
  - "form, non rettangolari"
  - "form, arrotondate"
  - "form con forme"
  - "Windows Form, circolari"
  - "Windows Form, forme personalizzate"
  - "Windows Form, forma non rettangolare"
  - "Windows Form, arrotondate"
  - "Windows Form, modellato"
ms.assetid: 6e6041e0-8e67-4487-b1e9-e410dbd1ef6c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare un Windows Form con una forma
Nell'esempio riportato di seguito viene attribuita al form una forma ellittica che viene ridimensionata con il form.  
  
## Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#10](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#10)]
 [!code-csharp[System.Drawing.ConceptualHowTos#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#10)]
 [!code-vb[System.Drawing.ConceptualHowTos#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#10)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli spazi dei nomi <xref:System.Windows.Forms> e <xref:System.Drawing>.  
  
 Nell'esempio viene eseguito l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> per modificare la forma del form.  Per utilizzare questo codice, copiare la dichiarazione di metodo e il codice di disegno all'interno del metodo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 <xref:System.Drawing.Region>   
 <xref:System.Drawing>   
 <xref:System.Drawing.Drawing2D.GraphicsPath.AddEllipse%2A>   
 <xref:System.Windows.Forms.Control.Region%2A>   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)