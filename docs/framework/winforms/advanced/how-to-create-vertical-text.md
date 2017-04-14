---
title: "Procedura: creare testo verticale | Microsoft Docs"
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
  - "stringhe [Windows Form], creazione in verticale"
  - "testo [Windows Form], creazione in verticale"
  - "testo verticale, disegno"
  - "Windows Form, disegno di testo verticale"
ms.assetid: 50c69046-4188-47d9-b949-cc2610ffd337
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare testo verticale
È possibile utilizzare un oggetto <xref:System.Drawing.StringFormat> per specificare che il testo venga rappresentato in verticale anziché in orizzontale.  
  
## Esempio  
 Nell'esempio riportato di seguito viene assegnato il valore <xref:System.Drawing.StringFormatFlags> alla proprietà <xref:System.Drawing.StringFormat.FormatFlags%2A> di un oggetto <xref:System.Drawing.StringFormat>.  Tale oggetto <xref:System.Drawing.StringFormat> viene poi passato al metodo <xref:System.Drawing.Graphics.DrawString%2A> della classe <xref:System.Drawing.Graphics>.  Il valore <xref:System.Drawing.StringFormatFlags> è un membro dell'enumerazione <xref:System.Drawing.StringFormatFlags>.  
  
 Nell'illustrazione che segue è visibile il testo verticale.  
  
 ![Testo caratteri](../../../../docs/framework/winforms/advanced/media/csfontstext5.png "csfontstext5")  
  
 [!code-csharp[System.Drawing.FontsAndText#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.FontsAndText#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#31)]  
  
## Compilazione del codice  
  
-   L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e` , un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Procedura: creare testo con GDI](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)