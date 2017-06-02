---
title: "Procedura: enumerare i tipi di carattere installati | Microsoft Docs"
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
  - "esempi [Windows Form], tipi di carattere"
  - "tipi di carattere, enumerazione installata"
ms.assetid: 26d74ef5-0f39-4eeb-8d20-00e66e014abe
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: enumerare i tipi di carattere installati
La classe <xref:System.Drawing.Text.InstalledFontCollection> eredita dalla classe di base astratta <xref:System.Drawing.Text.FontCollection>.  È possibile utilizzare un oggetto <xref:System.Drawing.Text.InstalledFontCollection> per enumerare i caratteri installati nel computer.  La proprietà <xref:System.Drawing.Text.FontCollection.Families%2A> di un oggetto <xref:System.Drawing.Text.InstalledFontCollection> corrisponde a una matrice di oggetti <xref:System.Drawing.FontFamily>.  
  
## Esempio  
 Con l'esempio riportato di seguito vengono elencati i nomi di tutti i gruppi di caratteri installati sul computer.  Viene recuperata la proprietà <xref:System.Drawing.FontFamily.Name%2A> di ciascun oggetto <xref:System.Drawing.FontFamily> nella matrice restituita dalla proprietà <xref:System.Drawing.Text.FontCollection.Families%2A>.  Una volta recuperati, i nomi dei gruppi vengono concatenati per formare un elenco separato da virgole.  Quindi, tramite il metodo <xref:System.Drawing.Graphics.DrawString%2A> della classe <xref:System.Drawing.Graphics>, l'elenco separato da virgole viene visualizzato in un rettangolo.  
  
 Se si esegue il codice di esempio, l'output sarà analogo a quello mostrato nell'illustrazione seguente.  
  
 ![Tipi di caratteri installati](../../../../docs/framework/winforms/advanced/media/csfontstext6.png "csfontstext6")  
  
 [!code-csharp[System.Drawing.FontsAndText#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.FontsAndText#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  Inoltre, è necessario importare lo spazio dei nomi <xref:System.Drawing.Text>.  
  
## Vedere anche  
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)