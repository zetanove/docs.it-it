---
title: "Procedura: disegnare testo verticale in un Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "StringFormat.FormatFlags"
  - "Graphics.DrawString"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "stringhe [Windows Form], creazione in verticale"
  - "testo [Windows Form], disegno"
  - "testo [Windows Form], creazione in verticale"
  - "testo [Windows Form], testo verticale"
ms.assetid: 717a6131-00f6-4373-b574-9894e8317799
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: disegnare testo verticale in un Windows Form
L'esempio di codice seguente mostra come disegnare testo verticale in un form utilizzando il metodo <xref:System.Drawing.Graphics.DrawString%2A> di <xref:System.Drawing.Graphics>.  
  
## Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#8](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#8)]
 [!code-csharp[System.Drawing.ConceptualHowTos#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#8)]
 [!code-vb[System.Drawing.ConceptualHowTos#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#8)]  
  
## Compilazione del codice  
 Non è possibile chiamare questo metodo nel gestore eventi <xref:System.Windows.Forms.Form.Load>.  Se il form viene ridimensionato o nascosto da un altro form, il contenuto creato non verrà ricreato.  Per ridisegnare automaticamente il contenuto è necessario eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il tipo di carattere Arial non viene installato.  
  
## Vedere anche  
 <xref:System.Drawing.Graphics.DrawString%2A>   
 <xref:System.Drawing.StringFormat.FormatFlags%2A>   
 <xref:System.Drawing.StringFormatFlags>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)